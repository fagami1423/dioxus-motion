> [!CAUTION]
> This library is under heavy development! It is not ready to use. Proceed at your own risk.

# Dioxus Motion 🚀

A lightweight, cross-platform animation library for Dioxus, designed to bring smooth, flexible animations to your Rust web, desktop, and mobile applications.

## ✨ Features

- **Cross-Platform Support**: Works on web (WASM), desktop, and mobile (I Guess ?)
- **Flexible Animation Configuration**
- **Custom Easing Functions**
- **Modular Feature Setup**
- **Simple, Intuitive API**

## 🛠 Installation

Add to your `Cargo.toml`:

```toml
[dependencies]
dioxus-motion = { 
    git = "https://github.com/wheregmis/dioxus-motion.git", 
    branch = "main", 
    optional = true 
}

[features]
default = ["web"]
web = ["dioxus/web", "dioxus-motion/wasm"]
desktop = ["dioxus/desktop", "dioxus-motion/desktop"]
mobile = ["dioxus/mobile"]
```

## 🌐 Platform Support

Choose the right feature for your platform:

- `web`: For web applications using WASM
- `desktop`: For desktop applications
- `mobile`: For mobile applications
- `default`: Web support (if no feature specified)

## 🚀 Quick Start

### Basic Web Animation

```rust
use dioxus::prelude::*;
use dioxus_motion::{Motion, use_motion};
use instant::Duration;

fn AnimatedComponent() -> Element {
    let mut motion = use_motion(
        Motion::new(0.0)
            .to(100.0)
            .duration(Duration::from_secs(2))
    );

    rsx! {
        div {
            "Value: {motion.value()}",
            button { 
                onclick: move |_| motion.start(), 
                "Animate" 
            }
        }
    }
}
```

### Desktop and Mobile Usage

The same code works across platforms - just enable the appropriate feature.

## 🎨 Advanced Usage

### Custom Easing and Completion Callback

```rust
use easer::functions::Bounce;

   let mut width_motion = use_motion(
        Motion::new(0.0)
            .to(100.0)
            .duration(Duration::from_millis(1500))
            .easing(Bounce::ease_in_out)
            .on_complete(|| println!("Complex animation complete!")),
    );
```

## 🛠 Configuration Options

- `.to(value)`: Set target animation value
- `.duration(Duration)`: Set animation duration
- `.easing(function)`: Specify custom easing function
- `.on_complete(callback)`: Add completion callback

## 🌈 Supported Easing Functions

Leverages the `easer` crate, supporting:
- Linear
- Quadratic
- Cubic
- Quartic
- And more!

## 💻 Example Project Configurations

### Web Project
```toml
[dependencies]
dioxus = "0.4"
dioxus-motion = { 
    git = "https://github.com/wheregmis/dioxus-motion.git", 
    features = ["web"] 
}
```

### Desktop Project
```toml
[dependencies]
dioxus = "0.4"
dioxus-motion = { 
    git = "https://github.com/wheregmis/dioxus-motion.git", 
    features = ["desktop"] 
}
```

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch
3. Commit changes
4. Push to the branch
5. Create a Pull Request

## 📄 License

MIT License

## 🐞 Reporting Issues

Please report issues on the GitHub repository with:
- Detailed description
- Minimal reproducible example
- Platform and feature configuration used

## 🌟 Motivation

Bringing elegant, performant motion animations to Rust's web and desktop ecosystems with minimal complexity.