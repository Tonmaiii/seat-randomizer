<script lang="ts">
    export let params: { number: string }

    function permutation(n: bigint, arr: number[]) {
        // Creating an empty stack
        let s: bigint[] = []
        let result: number[] = []

        // Subtracting 1 from N because the
        // permutations start from 0 in
        // Factoradic method
        n = n - 1n

        // Loop to generate the factroid
        // of the sequence
        for (let i = 1n; i < arr.length + 1; i++) {
            s.push(n % i)
            n = n / i
        }

        // Loop to generate nth permutation
        let len = arr.length
        for (let i = 0; i < len; i++) {
            let a = Number(s[s.length - 1])
            result.push(arr[a])
            let j = a

            // Remove 1-element in each cycle
            for (; j < arr.length; j++) {
                arr = [...arr.slice(0, j), arr[j + 1], ...arr.slice(j + 1)]
            }

            arr = arr.slice(0, j + 1)

            s.pop()
        }
        return result
    }

    const base64ToBigint = (s: string) => {
        const digits =
            '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ-_'
        return s
            .split('')
            .reverse()
            .reduce((sum, n) => (sum << 6n) + BigInt(digits.indexOf(n)), 0n)
    }

    const numbers = permutation(
        base64ToBigint(params.number),
        new Array(32).fill(0).map((_, i) => i + 1)
    )

    const seats = [
        numbers.slice(0, 7),
        numbers.slice(7, 14),
        numbers.slice(14, 21),
        numbers.slice(21, 28),
        [null, null, ...numbers.slice(28, 32), null]
    ]
</script>

<div class="container">
    {#each seats as row}
        <div class="row">
            {#each row as number}
                {#if number === null}
                    <div class="empty" />
                {/if}
                {#if number !== null}
                    <div class="item">{number}</div>
                {/if}
            {/each}
        </div>
    {/each}
</div>

<style>
    div.container {
        display: flex;
        flex-direction: column;
    }

    div.row {
        display: flex;
        flex-direction: row;
        justify-content: center;
    }

    div.item {
        display: flex;
        font-size: 4rem;
        width: 8rem;
        height: 8rem;
        align-items: center;
        justify-content: center;
        background-color: rgb(238, 238, 238);
        margin: 1rem;
    }

    div.empty {
        display: flex;
        width: 8rem;
        height: 8rem;
        margin: 1rem;
    }
</style>
