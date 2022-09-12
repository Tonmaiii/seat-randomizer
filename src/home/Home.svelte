<script lang="ts">
    const fact = (n: number): bigint =>
        new Array(n).fill(0).reduce((a, _, i) => (BigInt(i) + 1n) * a, 1n)

    const random = () => {
        const random = new Array(32)
            .fill(0)
            .reduce(
                (sum, _, i) =>
                    sum + BigInt(Math.floor(Math.random() * i)) * fact(i),
                0n
            )
        return random
    }

    const base64 = (n: bigint) => {
        const digits =
            '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ-_'
        if (n === 0n) return '0'
        let ans = ''
        while (n !== 0n) {
            const ch = n & 63n
            n >>= 6n
            ans = digits[Number(ch)] + ans
        }
        return ans
    }

    let text = ''

    const generate = () => {
        if (location.hash === '#/skip') {
            location.hash = `/display/${base64(random())}`
            return
        }
        setTimeout(() => (text = 'Spinning the wheel'), 0)
        setTimeout(() => (text = 'Actually its done a long time ago'), 4000)
        setTimeout(() => (text = "I'm just wasting everyone's time"), 6000)
        setTimeout(() => (text = "Let's actually finish now"), 8000)
        setTimeout(
            () => (location.hash = `/display/${base64(random())}`),
            10000
        )
    }
</script>

<div>
    <button on:click={generate}>Generate</button>
    <p>{text}</p>
</div>

<style>
    div {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 100%;
        height: 100%;
    }

    button {
        font-size: 5rem;
        color: black;
    }

    p {
        font-size: 1.5rem;
    }
</style>
