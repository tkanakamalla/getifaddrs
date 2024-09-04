# ifaddrs

A cross-platform library for retrieving network interface information.

This crate provides a simple and consistent API for querying network interface details
across different operating systems. It supports Unix-like systems (Linux, macOS, *BSD)
and Windows.

## Features

- Retrieve network interface information (name, IP address, netmask, flags, etc.)
- Filter interfaces based on various criteria (loopback, IPv4/IPv6, name, index)
- Cross-platform support (Unix-like systems and Windows)

## Usage

Add this to your `Cargo.toml`:

```toml
[dependencies]
ifaddrs = "0.1"
```

## Example

```rust
use ifaddrs::{getifaddrs, InterfaceFlags};

fn main() -> std::io::Result<()> {
    for interface in getifaddrs()? {
        println!("Interface: {}", interface.name);
        println!("  Address: {}", interface.address);
        if let Some(netmask) = interface.netmask {
            println!("  Netmask: {}", netmask);
        }
        println!("  Flags: {:?}", interface.flags);
        if interface.flags.contains(InterfaceFlags::UP) {
            println!("  Status: Up");
        } else {
            println!("  Status: Down");
        }
        println!();
    }
    Ok(())
}
```

## License

This project is licensed under the MIT License.
