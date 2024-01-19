Helium Gateway custom compile to overcome some slow signing CPU from Kerlink Helium Miner. My focus was to use as much as possible all the hardware features available in Cortex-A9 single core ARMv7.
Compiled on OracleCloudInfractucture VM.Standard3.Flex (Intel) instance (4cores, 16GB RAM). Ive used a custom Arch Linux and rust with cross compiling for target armv7-unknown-linux-musleabihf.

**Some commands for history and refference as your OS and versions could be different:**

$ cat .cargo/config.toml 
[target.armv7-unknown-linux-musleabihf]
rustflags = [
  "-C", "target-cpu=cortex-a9",
  "-C", "target-feature=+aclass,+neon,+sha2,+v7,+vfp3,+crt-static",
  "-C", "link-args=-static",
]
$

cargo install cross --git https://github.com/cross-rs/cross

cross build --target armv7-unknown-linux-musleabihf --release
or
cross build --target armv7-unknown-linux-gnueabihf --release

**Kerlink info from console:**
_cat /proc/cpuinfo 
processor	: 0
model name	: ARMv7 Processor rev 10 (v7l)
BogoMIPS	: 6.00
Features	: half thumb fastmult vfp edsp neon vfpv3 tls vfpd32 
CPU implementer	: 0x41
CPU architecture: 7
CPU variant	: 0x2
CPU part	: 0xc09
CPU revision	: 10

Hardware	: Freescale i.MX6 SoloX (Device Tree)
Revision	: 0000
Serial		: 0000000000000000_

tail -f /user/helium_gateway/log/helium_gateway.log

releases folder have some precompiled generic binaries. No Kerlink TZ as there is no open source for those. Use kerlink_musleabihf as the best optimised code for the Kerlink slow cpu.

All the best!73!
Chris/YO3TCO
