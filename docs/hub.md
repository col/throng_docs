# Throng Hub

**The Throng Hub is a centralized authentication portal that connects you to your Throng instance from anywhere.**

Register your self-hosted instance with the Hub and you'll get secure, authenticated access on your own subdomain — for example, `https://my-throng.throng.dev` — without having to expose your machine to the internet.

---

## What the Hub gives you

- **Your own subdomain.** Access your instance at `https://<your-name>.throng.dev` from any device.
- **Secure VPN tunnel.** The Hub establishes a tunnel to your self-hosted instance, so it's reachable from anywhere — even when it's running on a Mac Mini behind your home router.
- **Authentication built in.** Only you, and the teammates you explicitly grant access to, can reach your instance.
- **Work from anywhere.** Kick off tasks, review plans, and ship PRs from your laptop, phone, or a borrowed machine.

---

## Cloud hosting

Don't want to run Throng yourself? The Hub also offers managed cloud hosting, so you can be up and running in a few minutes — no hardware, no setup.

### Instance sizes

| Size   | vCPU | RAM   |
|--------|------|-------|
| Small  | 1    | 2 GB  |
| Medium | 2    | 4 GB  |
| Large  | 4    | 8 GB  |

Need more? Larger sizes are available on request.

### Picking a size

The right size depends on the size of your project(s) and how many Claude sessions you want to run concurrently. Throng lets you cap concurrency — for example, you can configure a limit of 3 development sessions at a time, and any additional sessions are queued and started automatically as capacity frees up.

If you're running on a larger instance — or self-hosting on something powerful like a well-spec'd Mac Mini — you can run far more sessions in parallel.

---

## How it works

1. **Sign in to the Hub** at [hub.throng.dev](https://hub.throng.dev).
2. **Register your instance.** The Hub assigns you a subdomain and provisions a secure tunnel.
3. **Invite teammates.** Grant access to collaborators so they can reach your instance under the same authenticated session.
4. **Access from anywhere.** Open your subdomain in any browser — the Hub authenticates you and routes traffic to your instance over the tunnel.
