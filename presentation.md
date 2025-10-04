---
theme:
  name: tokyonight-storm
  override:
    footer:
      style: template
      left: "@orhun.dev"
      right: "Tokyo Rust Meetup"
---

<!-- new_lines: 1 -->

![image:width:50%](assets/rat-dance-2.gif)

<!-- no_footer -->

<!-- end_slide -->

![image:width:35%](assets/rust-tokyo.png)

<!-- alignment: center -->

**Building Pocket-Sized Terminal UIs with Rust** 🦀

_Rust Tokyo Meetup 🇯🇵_

---

**Orhun Parmaksız**

`@orhun.dev` | `@ratatui.rs`

<!-- no_footer -->

<!-- end_slide -->

<!-- column_layout: [1, 1] -->

<!-- column: 0 -->

![image:width:80%](assets/rat-cook.png)

<!-- column: 1 -->

<!-- new_lines: 2 -->

# **Orhun Parmaksız**

🇹🇷 Creator based in **Ankara, Türkiye**

🦀 _Open source, Rust and terminals!_

🐭 **Ratatui**, **Ratzilla**, **git-cliff** ...

📦 **Arch Linux** (btw)

---

`https://github.com/orhun`  
`https://youtube.com/@orhundev`

<!-- end_slide -->

<!-- alignment: center -->

<!-- new_lines: 3 -->

**Imagine a rat.**

<!-- pause -->

![](assets/rat-cup.gif)

<!-- pause -->

_rat wants to download MP3_

<!-- pause -->

_rat goes to ytmp3downloader.cc_

<!-- no_footer -->

<!-- end_slide -->

![image:width:100%](assets/yy-info.gif)

<!-- pause -->

<!-- jump_to_middle -->

![](assets/rat-cry.gif)

<!-- alignment: center -->

<!-- no_footer -->

<!-- end_slide -->

<!-- no_footer -->

<!-- alignment: center -->

<!-- new_lines: 3 -->

**Imagine a rat (again)**

![](assets/rat-cup-2.gif)

<!-- pause -->

_rat wants to find the cheese.txt_

<!-- pause -->

_rat uses file search_

<!-- end_slide -->

<!-- no_footer -->

![image:width:40%](assets/loading-bar.png)

<!-- pause -->

![](assets/loading-bar-1.png)

<!-- pause -->

![](assets/loading-bar-2.png)

<!-- pause -->

<!-- jump_to_middle -->

![](assets/rat-tired.gif)

<!-- end_slide -->

<!-- alignment: center -->

<!-- new_lines: 3 -->

<!-- no_footer -->

**Imagine a rat (sorry)**

![](assets/rat-sus.gif)

<!-- pause -->

_rat wants to monitor network traffic_

<!-- pause -->

_rat runs a GUI tool_

<!-- pause -->

<!-- end_slide -->

<!-- no_footer -->

![image:width:60%](assets/clicking.gif)

<!-- end_slide -->

![image:width:40%](assets/rat-boom.gif)

<!-- alignment: center -->

_rat explodes._

<!-- no_footer -->

<!-- end_slide -->

# Solution?

<!-- pause -->

The terminal.

<!-- pause -->

```bash
$ yt-dlp -f bestaudio --extract-audio --audio-format mp3
```

<!-- pause -->

```bash +exec +acquire_terminal
ig 'fn main' /home/orhun/gh/
```

<!-- pause -->

```sh +exec +acquire_terminal
sudo oryx -i wlp3s0
```

<!-- end_slide -->

![image:width:80%](assets/ratatui-header.png)

<!-- alignment: center -->

**https://ratatui.rs**

<!-- pause -->

---

> Ratatui is a Rust library for cooking up terminal user interfaces (TUIs).

- Been around since `2023` (fork of `tui-rs`)

- `250+` contributors, hundreds of apps, `8M+` crate downloads

- `tokio-console`, `yazi`, `dioxus-cli`, `atuin`, `gitui` & more

- Used by `Netflix`, `OpenAI`, `OVHcloud` & many more

<!-- end_slide -->

```bash +exec +acquire_terminal
cargo run --manifest-path ratatui/examples/apps/demo2/Cargo.toml
```

<!-- end_slide -->

# atac

<!-- alignment: center -->

Postman-like API client for the terminal.

![image:width:90%](assets/atac.gif)

[](https://github.com/Julien-cpsn/ATAC)

<!-- end_slide -->

# doxx

<!-- alignment: center -->

View .docx files in the terminal.

![image:width:90%](assets/doxx.gif)

[](https://github.com/bgreenwell/doxx)

<!-- end_slide -->

# rebels-in-the-sky

<!-- alignment: center -->

Spacepirates playing basketball across the galaxy

[](https://github.com/ricott1/rebels-in-the-sky)

---

<!-- pause -->

```bash +exec +acquire_terminal
rebels-in-the-sky
```

<!-- end_slide -->

# sharad-ratatui

<!-- alignment: center -->

A text-based Shadowrun role-playing game.

[](https://github.com/ProHaller/sharad_ratatui)

---

<!-- pause -->

```bash +exec
mpv assets/sharad.mp4 > /dev/null 2>&1
```

<!-- end_slide -->

# grainiac

<!-- alignment: center -->

Granular sampler that has a terminal user interface.

[](https://github.com/christian-grothe/grainiac)

---

<!-- pause -->

```bash +exec
mpv assets/grainiac.mp4 > /dev/null 2>&1
```

<!-- pause -->

```bash +exec
handlr open https://www.youtube.com/watch?v=XzJnMVo1ZkM
```

<!-- end_slide -->

# tachyonfx

<!-- alignment: center -->

Add shader-like effects to your terminal applications.

[](https://github.com/junkdog/tachyonfx)

---

<!-- pause -->

```bash +exec +acquire_terminal
exabind
```

<!-- end_slide -->

<!-- alignment: center -->

<!-- new_lines: 2 -->

![](assets/rat-demand.gif)

<!-- no_footer -->

_Show me!_

<!-- end_slide -->

<!-- column_layout: [1, 1] -->

<!-- column: 0 -->

## Widgets

- Block
- BarChart
- Calendar
- Canvas
- Chart
- Gauge
- LineGauge
- List
- Paragraph
- Scrollbar
- Sparkline
- Table
- Tabs
- ...

- Anything that implements `Widget` trait

<!-- column: 1 -->

<!-- pause -->

## Key Concepts

- Rendering
- Layout
- Event handling

![image:width:60%](assets/ratcopter.gif)

<!-- end_slide -->

### Minimal example

```rust {1-20|5|6|7,16-18|8-11|12-14|1-20} +line_numbers
use ratatui::crossterm::event::{self, Event};
use ratatui::{text::Text, Frame};

fn main() -> std::io::Result<()> {
    let mut terminal = ratatui::init();
    loop {
        terminal.draw(draw)?;
        if matches!(event::read()?, Event::Key(_)) {
            break;
        }
    }
    ratatui::restore();
    Ok(())
}

fn draw(frame: &mut Frame) {
    frame.render_widget("Hello World!", frame.area());
}
```

<!-- end_slide -->

### Even more minimal example

```rust {1-13|2|3|4-6|8-10|1-13} +line_numbers
fn main() -> std::io::Result<()> {
    ratatui::run(|terminal| {
        loop {
            terminal.draw(|frame|
                frame.render_widget("rat", frame.area())
            )?;

            if crossterm::event::read()?.is_key_press() {
                break Ok(());
            }
        }
    })
}
```

<!-- end_slide -->

### 1. Rendering

<!-- pause -->

<!-- column_layout: [3, 1] -->

<!-- column: 0 -->

```rust {1-16|1|1,4,9|6,11|1-16} +line_numbers
let mut toggle = false;
loop {
    terminal.draw(|frame: &mut Frame| {
        if toggle {
            frame.render_widget(
                BarChart::default()
                //...
            );
        } else {
            frame.render_widget(
                LineGauge::default()
                //...
            );
        }
    });
}
```

<!-- column: 1 -->

<!-- new_lines: 6 -->

![](assets/rat-dance2.gif)

<!-- end_slide -->

### 2. Layout

<!-- pause -->

<!-- column_layout: [8, 2] -->

<!-- column: 1 -->

<!-- new_lines: 11 -->

![](assets/rat-point.gif)

<!-- column: 0 -->

```rust {1-9|2|3-7|1-9} +line_numbers
let layout = Layout::default()
    .direction(Direction::Horizontal)
    .constraints(&[
        Constraint::Length(10),
        Constraint::Percentage(70),
        Constraint::Min(5),
    ])
    .split(frame.area());
```

<!-- pause -->

```rust +line_numbers
let percent =
  if msg_count > 50 { 80 } else { 50 };

let contraints = &[
  Constraint::Percentage(percent),
  Constraint::Percentage(100 - percent)
];
```

<!-- end_slide -->

#### Constraints

```bash +exec +acquire_terminal
cd ratatui
cargo run -p constraint-explorer
```

<!-- pause -->

#### Flex

```bash +exec +acquire_terminal
cd ratatui
cargo run -p flex
```

<!-- end_slide -->

### 3. Event Handling

<!-- pause -->

- Backends: `crossterm`, `termion`, `termwiz` & 3rd party

<!-- pause -->

#### Strategies

- Centralized event handling
- Centralized catching, message passing
- Distributed event loops/segmented applications

<!-- new_lines: 1 -->

![image:width:25%](assets/rat-ski.gif)

<!-- end_slide -->

# Architecture (>=v0.30)

<!-- column_layout: [1, 1, 1] -->

<!-- column: 0 -->

### Widgets

- BarChart
- Calendar
- Canvas
- Chart
- Sparkline
- Table
- `impl Widget`
- ...

<!-- column: 1 -->

### Backends

- Crossterm
- Termion
- Termwiz
- `impl Backend`

<!-- column: 2 -->

### Components

ratatui  
├── `ratatui-core`  
├── `ratatui-widgets`  
├── ratatui-crossterm  
├── ratatui-termion  
├── ratatui-termwiz  
└── ratatui-macros

<!-- reset_layout -->

<!-- alignment: center -->

![image:width:12%](assets/rat-noted.gif)

<!-- pause -->

_So why shall we stop here?_

<!-- end_slide -->

<!-- alignment: center -->

![](assets/suzui-rs.jpg)

Ratatui on `Suzuki Baleno`  
[](https://github.com/thatdevsherry/suzui-rs)

<!-- end_slide -->

<!-- new_lines: 1 -->

![image:width:100%](assets/ratatui-psp.png)

<!-- alignment: center -->

Ratatui on `PSP`  
`https://github.com/overdrivenpotato/rust-psp/pull/190`

<!-- end_slide -->

<!-- new_lines: 1 -->

We call this:

<!-- pause -->

![image:width:70%](assets/ratatuify.png)

<!-- alignment: center -->

_https://www.urbandictionary.com/define.php?term=ratatuify_

<!-- pause -->

_But how is it possible?_ 🤔

<!-- end_slide -->

### impl Backend

```rust
pub trait Backend {
    fn draw<'a, I>(&mut self, content: I) -> Result<()>
       where I: Iterator<Item = (u16, u16, &'a Cell)>;
    fn hide_cursor(&mut self) -> Result<()>;
    fn show_cursor(&mut self) -> Result<()>;
    fn get_cursor_position(&mut self) -> Result<Position>;
    fn set_cursor_position<P: Into<Position>>(
        &mut self,
        position: P,
    ) -> Result<()>;
    fn clear(&mut self) -> Result<()>;
    fn size(&self) -> Result<Size>;
    fn window_size(&mut self) -> Result<WindowSize>;
    fn flush(&mut self) -> Result<()>;
    // ...
}
```

<!-- end_slide -->

### Custom Backends

| Repository                          | Description                                 |
| ----------------------------------- | ------------------------------------------- |
| _reubeno_/`ratatui-uefi`            | UEFI                                        |
| _j-g00da_/`mousefood`               | embedded-graphics backend                   |
| _Jesterhearts_/`ratatui-wgpu`       | GPU-accelerated rendering to a buffer       |
| _gold-silver-copper_/`egui_ratatui` | EGUI widget                                 |
| _gold-silver-copper_/`soft_ratatui` | Pure software rendering to arbitrary buffer |
| _cxreiff_/`bevy_ratatui_camera`     | Render Bevy app to the terminal             |
| _orhun_/`ratzilla`                  | Web                                         |

![](assets/rat-point.gif)

<!-- new_lines: 1 -->

<!-- end_slide -->

#### Example: Ratzilla

Build terminal-themed web applications with Rust and WebAssembly.

Supports:

- `CanvasBackend`
- `DomBackend`
- `WebGl2Backend`

---

<!-- pause -->

```bash +exec
handlr open https://orhun.dev/ratzilla/demo/
```

<!-- end_slide -->

Today we will talk about:

<!-- pause -->

![](assets/rat-cheese.gif)

![image:width:87%](assets/mousefood-demo.gif)

<!--alignment: center-->

_mousefood_!

<!-- end_slide -->

⚠️ Make sure you have all the tools installed:

```bash
git clone https://github.com/orhun/embedded-ratatui-workshop
```

<!-- pause -->

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

source $HOME/.cargo/env

cargo install espup
espup install

. ~/export-esp.sh

cargo install espflash ldproxy
```

<!-- end_slide -->

# Know your hardware!

**ESP32 T-Display**

| Feature               | Specification                                 |
| --------------------- | --------------------------------------------- |
| MCU                   | ESP32 Xtensa dual-core LX6 microprocessor     |
| CPU                   | Xtensa dual-core LX6 @ up to 240 MHz          |
| RAM                   | 520 KB SRAM (typical for ESP32)               |
| Wireless Connectivity | Wi-Fi 802.11 b/g/n, BL V4.2 + BLE             |
| Serial Chip           | CH9102                                        |
| Optional              | Flash: 4M / 16M                               |
| Onboard Functions     | Buttons: l006 + I007, battery power detection |
| Display               | 1.14" 135x240px IPS LCD, ST7789V controller   |

<!-- column_layout: [1, 1, 1]-->

<!-- column: 0 -->

<!-- new_lines:  2-->

![image:width:100%](assets/esp32.gif)

<!-- column: 1 -->

![](assets/esp32-wroom-32d.gif)

<!-- column: 2 -->

![](assets/t-display.png)

<!-- end_slide -->

# Frameworks

<!-- column_layout: [1, 1] -->
<!-- column: 0 -->

## **esp-hal**

- Bare metal (`#![no_std]`)
- Development funded by Espressif

<!-- column: 1 -->

## **esp-idf-hal**

- With `std` support!
- Community effort
- Requires a custom toolchain

<!-- reset_layout -->

<!-- column_layout: [2, 3] -->
<!-- column: 0 -->

<!-- pause -->

## Toolchain

```sh
cargo install espup
espup install
```

```sh
cargo install espflash
```

<!-- column: 1 -->

<!-- pause -->

`.cargo/config.toml`:

```toml
[build]
target = "xtensa-esp32-espidf"

[target.xtensa-esp32-espidf]
linker = "ldproxy"
runner = "espflash flash --monitor"
rustflags = [ "--cfg",  "espidf_time64"]
```

<!-- end_slide -->

### Ratatui + embedded-graphics = **Mousefood**

<!-- column_layout: [4, 3] -->

<!-- column: 0 -->

- Built on `embedded-graphics`
- Custom bitmap font support

<!-- column: 1 -->

![image:width:40%](assets/mousefood.gif)

<!-- reset_layout -->

```rust {1-9|2|4|5|7-9|1-9}
// Any embedded_graphics DrawTarget
let mut display = MyDrawTarget::new();

let backend = EmbeddedBackend::new(&mut display, EmbeddedBackendConfig::default());
let mut terminal = Terminal::new(backend)?;

loop {
    terminal.draw(...)?;
}
```

<!-- alignment: center -->

`https://github.com/j-g00da/mousefood`

<!-- end_slide -->

<!-- alignment: center -->

Try out:

```bash
cd template
cargo run --release
```

Or:

```bash
espflash flash --monitor apps/binaries/mousefood-demo.bin
```

![](assets/rat-ski.gif)

<!-- end_slide -->

### Simulator 🤖

```rust {1-15|1-8|10|12-13|15|1-15}
let mut simulator_window = Window::new(
    "mousefood simulator",
    &OutputSettings {
        scale: 4,
        max_fps: 30,
        ..Default::default()
    },
);

let mut display = SimulatorDisplay::new(Size::new(128, 64));

let config = EmbeddedBackendConfig::default();
let backend = EmbeddedBackend::new(&mut display, config);

let mut terminal = Terminal::new(backend)?;
```

<!-- alignment: center -->

Starts Ratatui with the simulator backend

<!-- end_slide -->

<!-- alignment: center -->

Run the simulator:

```bash
cd apps/simulator
cargo run
```

(requires SDL2)

![](assets/rat-ski.gif)

<!-- end_slide -->

# Soo, what can we do?

<!-- pause -->

Learn guitar!

![](assets/pcb-works.jpg)

<!-- alignment: center -->

| _Powered by Rust, Ratatui and 9 volt battery!_

<!-- end_slide -->

![image:width:30%](assets/tuitar-logo.png)

<!-- alignment: center -->

"_A portable and terminal-based guitar training tool_"

![image:width:40%](assets/tuitar-case.png)

```sh +exec
mpv /home/orhun/downloads/tuitar-final.mp4
```

<!-- end_slide -->

<!-- new_lines: 1 -->

![image:width:80%](assets/rustforge-demo.png)

<!-- alignment: center -->

[](https://www.youtube.com/live/es48dmNWMVQ)

Live demo at Rust Forge!

<!-- end_slide -->

<!-- column_layout: [5, 8] -->

<!-- column: 0 -->

### impl Widget

```rust
pub struct Fretboard {
    tuning: Vec<Note>,
    style: Style,
}
```

```rust
pub struct FretboardState {
    notes: Vec<Note>
}
```

![](assets/rat-spin.gif)

<!-- column: 1 -->

```rust
impl StatefulWidget for &Fretboard {
    type State = FretboardState;

    fn render(
        self,
        area: Rect,
        buf: &mut Buffer,
        state: &mut Self::State,
    ) {
        for s in self.tuning.iter() {
            // ...
            buf.set_line(
                area.x,
                area.y + i as u16,
                &Line::from(spans),
                area.width,
            );
        }
    }
}
```

<!-- end_slide -->

## Introducing `ratatui-fretboard` widget 🎉

```rust
let fretboard = Fretboard::default();
let mut state = FretboardState::default();
state.set_active_note(Note::A(4));
frame.render_stateful_widget(fretboard, area, &mut state);
```

```
E4 ║─┼───┼───┼───┼───┼─⬤─┼───┼───┼───┼───┼───┼───║
B3 ║─┼───┼───┼───┼───┼───┼───┼───┼───┼───┼─⬤─┼───║
G3 ║─┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───║
D3 ║─┼───┼───┼─•─┼───┼─•─┼───┼─•─┼───┼─•─┼───┼───║
A2 ║─┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───║
E2 ║─┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───┼───║
     1   2   3   4   5   6   7   8   9  10  11  12
```

<!-- alignment: center -->

String names, frets, colors and everything else is customizable.

<!-- end_slide -->

![width:100%](assets/mountain-dew-guitar.jpg)

<!-- end_slide -->

```
D0 ║─┼───┼───┼─⬤─┼───┼─⬤─┼───┼───┼───┼─⬤─┼───┼───┼───┼───║
G0 ║─┼───┼───┼───┼─⬤─┼───┼───┼───┼───┼─⬤─┼───┼───┼───┼───║
C0 ║─┼───┼─⬤─┼───┼───┼─⬤─┼───┼─⬤─┼───┼───┼───┼─⬤─┼───┼───║
F0 ║─┼───┼─⬤─┼───┼───┼───┼─⬤─┼───┼───┼───┼───┼─⬤─┼───┼───║
B0 ║─┼───┼───┼───┼───┼─⬤─┼───┼───┼───┼───┼─⬤─┼───┼─•─┼───║
E1 ║─┼───┼───┼─•─┼───┼─⬤─┼───┼─•─┼───┼─•─┼─⬤─┼───┼───┼───║
A1 ║─┼───┼───┼───┼───┼─⬤─┼───┼───┼───┼───┼─⬤─┼───┼─•─┼───║
D2 ║─┼───┼───┼───┼───┼─⬤─┼───┼───┼───┼─✖─┼─⬤─┼───┼─✖─┼───║
G2 ║─┼───┼───┼───┼─✖─┼─⬤─┼───┼─✖─┼───┼───┼───┼───┼───┼───║
C3 ║─┼───┼─✖─┼───┼───┼───┼───┼───┼───┼─✖─┼───┼───┼───┼───║
     1   2   3   4   5   6   7   8   9  10  11  12  13  14
```

![](assets/rat-clown.gif)

<!-- end_slide -->

## TUItar

```sh +exec +acquire_terminal
tuitar
```

<!-- alignment: center -->

[](https://github.com/orhun/tuitar)

<!-- end_slide -->

<!-- alignment: center -->

<!-- new_lines: 3 -->

Want more?

![](assets/rat-demand.gif)

_Talk is cheap, show me the cheese._

<!-- end_slide -->

![](assets/irc-client.jpg)

<!-- alignment: center -->

[](https://github.com/intuis/mnyaoo32)

<!-- end_slide -->

<!-- column_layout: [1, 4, 4, 1] -->

<!-- column: 1 -->

![image:width:90%](assets/phone-os-1.png)

<!-- column: 2 -->

![image:width:90%](assets/phone-os-2.png)

<!-- reset_layout -->

<!-- alignment: center -->

[](https://github.com/Julien-cpsn/Phone-OS)

<!-- end_slide -->

### Animations

![image:width:100%](assets/s3-display.gif)

<!-- alignment: center -->

via [](https://github.com/junkdog/tachyonfx)

<!-- end_slide -->

<!-- new_lines: 3 -->

<!-- alignment: center -->

I think you have an idea now...

<!-- pause -->

![image:width:25%](assets/ratatui-spin.gif)

Workshop time!

<!-- no_footer -->

<!-- end_slide -->

<!-- new_lines: 2 -->

![image:width:45%](assets/lethimcook.gif)

<!-- no_footer -->

<!-- end_slide -->

## Check your kitchen setup

```bash
git clone https://github.com/orhun/embedded-ratatui-workshop
```

Make sure your tools work before we start cooking!

```bash
cd template
cargo run --release
```

<!-- alignment: center -->

✅ "Ratatui on embedded devices!" on screen

⚠️ If not, check the Troubleshooting section or ask a chef for help.

<!-- end_slide -->

```
.
├── build.rs             -> Build script
├── .cargo
│   └── config.toml      -> Cargo configuration for ESP32
├── Cargo.toml           -> Dependencies and metadata
├── rust-toolchain.toml  -> Specifies Rust toolchain
├── sdkconfig.defaults   -> ESP-IDF configuration
└── src
    ├── button.rs        -> Button handling module
    ├── lib.rs           -> Module definitions
    ├── main.rs          -> Main application
    └── setup.rs         -> Setup and initialization code
```

<!-- pause -->

<!-- alignment: center -->

We are mainly going to work in `src/main.rs`.

<!-- pause -->

It contains an implementation of `App` trait for the application lifecycle.

<!-- end_slide -->

## Add your own flavor

- Edit the `App::draw()` method.

- Try one of these:

  - Change the text
  - Add colors or borders
  - Experiment with layout
  - Render different widgets

🎨 Minimal widget examples: `https://github.com/ratatui/ratatui/tree/main/ratatui-widgets/examples`

📚 Widgets documentation: `https://docs.rs/ratatui/latest/ratatui/widgets/index.html`

---

To re-flash: `cargo run --release`

<!-- end_slide -->

## Cook your own dish!

Now that you've mastered the basics, create something fun!

🧠 Some ideas:

- Tamagotchi (Rat-agotchi?)
- Timer / Pomodoro
- Digital Fortune Cookie
- Reaction Game (like whack-a-mole)
- A mini game (like Snake or Tetris)
- ASCII pixel art (look into `Widget` trait)

<!-- pause -->

---

🧀 Show and tell!

<!-- end_slide -->

<!-- alignment: center -->

# Thank You, Little Chefs! 🐀

_ありがとうございました_

![](assets/rat-ending.gif)

Remember:  
_“Anyone can cook — and anyone can TUI.”_

<!-- end_slide -->

<!-- alignment: center -->

![image:width:30%](assets/real-ratatui.jpg)

<!-- new_lines: 1 -->

🐭 **Slides:** [](https://github.com/orhun/embedded-ratatui-talk)  
🧀 **Sponsor:** [](https://github.com/sponsors/orhun)  
📺 **More rats:** [](https://youtube.com/@orhundev)

✨ See you at the next workshop — and keep cooking.

`P.S. I don't have a rat under my hat!`
