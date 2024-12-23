# Dioxus Motion - Simple Animation Roadmap If i dont get bored?

# Dioxus Motion - Implementation Progress

## Phase 1: Core Animation Primitives
### Animate Component
- [x] Basic value transitions
  ```rust
  // Already implemented via:
  Motion::new(0.0)
      .to(100.0)
      .duration(Duration::from_millis(300))
  ```
- [x] Duration control
- [x] Easing functions
<-I think for the below option, we can have another crate as a layer which will abstract and build elements based on value, cause its just value that we put on these attributes->
- [ ] Common animation properties
  - [ ] x, y (transform)
  - [ ] scale
  - [ ] rotate
  - [ ] opacity

### Basic Transitions
- [x] Duration (implemented via `duration()`)
- [x] Easing functions (implemented via `easing()`)
- [x] Animation completion callbacks
- [x] Delay
- [x] Spring animations

## Phase 2: Animation State & Control
### State Management
- [x] Animation state tracking (Idle, Running, Completed)
- [x] Progress tracking
- [x] Running state detection

### Controls
- [x] Start animation  -> Will always start from the initial value
- [x] Stop   -> Will stop on the stopped value
- [x] Resume  -> Will continue from the stopped value
- [x] Reset animation  -> Will reset back to initial value

## Current Implementation Strengths
- ✅ Solid foundation for value animations
- ✅ Cross-platform support (Web/Desktop)
- ✅ Clean API design
- ✅ Good state management
- ✅ Performance consideration (frame rate control)

## Next Immediate Tasks
1. Transform Properties
```rust
// Target API
Motion::new(0.0)
    .x(100)
    .y(50)
    .scale(1.2)
    .rotate(45.0)
    .opacity(0.8)
```

2. Animation Controls
```rust
// Target API
let mut motion = use_motion(...);
motion.start();
motion.stop();
motion.resume();
motion.reset();
```

3. Delay Support
```rust
// Target API
Motion::new(0.0)
    .to(100.0)
    .delay(Duration::from_millis(500))
```

### Variants Taking the scope outside of core motion and provide maybe some overlay for it?
- [ ] Named animation states
  ```rust
  let variants = AnimationVariants::new()
      .add("open", Motion::new().scale(1).opacity(1))
      .add("closed", Motion::new().scale(0).opacity(0));
  
  rsx! {
      div {
          variants: variants,
          animate: "open",
      }
  }
  ```


## Example API (Target)  Taking the scope outside of core motion and provide maybe some overlay for it?
```rust
use dioxus_motion::prelude::*;

fn AnimatedComponent() -> Element {
    rsx! {
        // Simple animation
        div {
            animate: Motion::new()
                .x(100)
                .opacity(0.5)
                .duration(300),
            "Animated div"
        }

        // Hover animation
        button {
            whileHover: Motion::new()
                .scale(1.1)
                .duration(200),
            "Hover me"
        }

        // Variants
        div {
            variants: variants,
            animate: is_open.then(|| "open").unwrap_or("closed"),
            "Toggle me"
        }
    }
}
```

## Success Goals
- Simple, intuitive API
- Smooth animations
- Small bundle size
- Easy to understand documentation
- Basic but powerful feature set