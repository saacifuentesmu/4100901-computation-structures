# Computation Structures — UNAL 4100901

A course about **learning hardware**, using an **ARM Cortex-M4 (STM32L476RG)** and a
dev kit as the vehicle. Taught at the Universidad Nacional de Colombia, Sede
Manizales. The goal isn't the chip — it's understanding what's underneath it: how a
processor is built, how it talks to the world, and why the silicon behaves the way it
does. The ARM + NUCLEO board is just a concrete, accessible instrument for getting
there. *(An ideal version of this course would have students design their own
RISC-V core — same goal, deeper down the stack.)*

This is the course hub: the material lives across the repositories below, ordered the
way the semester runs.

The through-line is one system — a **room-control device** — built three times,
each time closer to a real product:

1. first **from bare registers** (no HAL), to understand the silicon;
2. then **rebuilt on the STM32 HAL / CubeMX** with modular, reusable drivers;
3. then **extended into a networked final project** — access control, climate
   control, and remote telemetry.

The midterm and the two hardware labs sit in between as checkpoints. Course
material is in Spanish; repo names and this overview are in English.

## First month — foundations (lectures)

The semester opens with three lecture sessions that set the context and review the
digital-systems background before any code is written:

1. **Intro — from microchip to MCU.** What an IC is and how it's fabricated
   (photolithography, doping), then processor → CPU → system bus → embedded
   systems → MCU / SoC / SiP, and the system clock.
2. **Digital circuits.** A digital-systems review — information and encoding, the
   digital abstraction (representing data with voltages in a noisy world), CMOS,
   and combinational devices. Follows MIT 6.004
   ([computationstructures.org](https://computationstructures.org/)).
3. **Programmable architectures.** How a computer is built and how C becomes a
   binary (preprocess → compile → assemble → link); Von Neumann vs Harvard; the
   ARM Cortex-A/R/M families; Cortex-M as a load/store machine; and the STM32L476
   memory layout and AHB bus matrix.

Session 3 leads directly into **assembly and bare-metal programming**, whose hands-on
material lives in the [bare-metal foundations repo](https://github.com/saacifuentesmu/4100901-1-bare-metal-foundations)
(`Doc/2_ASM_CONFIG.md`, `3_WORKSHOP_ASM.md`, `4_WORKSHOP_C.md`). The midterm opens
with a 20-minute [foundations quiz](https://github.com/saacifuentesmu/4100901-3-midterm-room-control/blob/main/QUIZ.md)
drawn from these three sessions.

The very first hands-on session is a guided
[intro practice](https://github.com/saacifuentesmu/4100901-Intro_Project) that doubles
as a dev-environment check: get the toolchain working (VS Code, STM32CubeMX, HAL) and
make the board respond to a button over UART — heartbeat LED, a 3 s "unlock" output,
and serial echo. It deliberately starts at the HAL/CubeMX level for a quick win; the
rest of the course then peels that abstraction back down to the registers.

## Course path

| # | Module | Repository | What it covers |
|---|--------|-----------|----------------|
| 0 | Setup — dev env & first blink | [4100901-Intro_Project](https://github.com/saacifuentesmu/4100901-Intro_Project) | First class: validate the toolchain (VS Code, CubeMX, HAL) with a guided intro — heartbeat LED, button-triggered 3 s "unlock", and UART echo on the NUCLEO-L476RG |
| 1 | Foundations — bare metal | [4100901-1-bare-metal-foundations](https://github.com/saacifuentesmu/4100901-1-bare-metal-foundations) | The STM32L476 from registers up: ARM ISA & assembly, clock tree, GPIO, EXTI/NVIC, SysTick, UART and TIM/PWM — no HAL |
| 2 | Lab 1 — peripherals | [4100901-2-peripherals-lab](https://github.com/saacifuentesmu/4100901-2-peripherals-lab) | Measuring the physical behaviour of peripherals: button RC settling, PWM frequency/duty, UART bit timing — with logic analyzer and scope |
| 3 | Midterm workshop | [4100901-3-midterm-room-control](https://github.com/saacifuentesmu/4100901-3-midterm-room-control) | Practical assessment: extend the room-control firmware (UART commands, PWM duty, door/occupancy state) |
| 4 | Project — HAL phase | [4100901-4-room-control-hal](https://github.com/saacifuentesmu/4100901-4-room-control-hal) | The same system rebuilt on CubeMX/HAL with modular drivers: ring buffers, hex keypad, SSD1306 OLED, ADC temperature, I2C |
| 5 | Lab 2 — drivers | [4100901-5-drivers-lab](https://github.com/saacifuentesmu/4100901-5-drivers-lab) | Driver-level work and optimization: OLED (SSD1306) frame timing over I2C, ESP-01 Wi-Fi, memory/time/energy trade-offs |
| 6 | Final project | [4100901-6-final-project](https://github.com/saacifuentesmu/4100901-6-final-project) | Remote access & climate control: keypad entry, OLED UI, temperature-driven PWM fan, ESP-01 TCP/IP remote console with a command parser |

## Hardware & tooling

NUCLEO-L476RG · STM32CubeMX + CubeCLT + CMake · VS Code · Saleae logic analyzer ·
Analog Discovery scope · YAT/PuTTY. Peripherals across the course: GPIO, EXTI/NVIC,
SysTick, TIM/PWM, USART, I2C, ADC, plus the SSD1306 OLED, a hex keypad, and the
ESP-01 Wi-Fi module.

## What it demonstrates

Hardware understanding taught through a single product that grows from register
access to a networked system — register-level fluency and HAL-based engineering side
by side, with modular drivers, instrumented measurement (logic analyzer / scope), and
design patterns carried through to the final project. The ARM dev kit is the
teaching instrument; the lasting takeaway is how the machine works underneath.

---

Maintained by Sam C · Universidad Nacional de Colombia, Sede Manizales.
