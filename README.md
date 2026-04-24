# oom.ai

**Pack the isolation stack. Don't get OOM-killed.**

A single-page arcade game about virtual machine isolation. You have 2 GiB of RAM and 13 isolation technologies — from `chroot` to QEMU full-PC emulation. Pack as many workloads as you can before the OOM killer comes.

## Play

Open `index.html` in a browser. That's it — no build, no server, no dependencies.

To host it: drop `index.html` anywhere that serves static files (GitHub Pages, S3, Netlify, `python -m http.server`, etc.).

## The 13 isolation types

| Category | Technology | MiB | Security |
|---|---|---|---|
| Shared kernel | chroot | 1 | 1/10 |
| Shared kernel | Container (runc) | 3 | 2/10 |
| Shared kernel | Hardened container | 5 | 3/10 |
| Shared kernel | Sysbox | 8 | 4/10 |
| Userspace iso | V8 Isolate | 3 | 5/10 |
| Userspace iso | WebAssembly | 5 | 6/10 |
| Userspace iso | gVisor | 15 | 6/10 |
| MicroVMs | Firecracker | 5 | 9/10 |
| MicroVMs | Cloud Hypervisor | 10 | 9/10 |
| MicroVMs | QEMU microvm | 32 | 9/10 |
| Feature VMs | Edera | 20 | 10/10 |
| Feature VMs | Kata Containers | 50 | 9/10 |
| Feature VMs | QEMU full PC | 128 | 10/10 |

## Scoring

- Base: `security_level × 10`
- Chain multiplier (×1.0 → ×5.0): grows when you alternate types, resets on repeats or 2.5s pause
- High score persists in `localStorage`
- Game ends when the next VM won't fit — OOM killer takes over

## Controls

- Click any palette card, or use keyboard: `1`–`0`, `q`, `w`, `e`
- `SPACE` — spawn a random type
- `R` — reset

## Credits

Numbers and framing paraphrased from [Emir Beganović's *MicroVM Isolation Landscape in 2026*](https://emirb.github.io/blog/microvm-2026/).

Full-PC QEMU is the bet [opencomputer.dev](https://opencomputer.dev) made — and why the expensive block is also the most flexible one.

No frameworks. No network. One HTML file.
