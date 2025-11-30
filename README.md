# ADF4158 + YSGM556006 Test Board  

**Thanks Mr GPT for (some parts of) the readme**

**5.5–6.0 GHz PLL/VCO Synthesizer w/ RP2040 Control**

This project is a small test board built around the **Analog Devices ADF4158** fractional-N PLL and the **Innotion YSGM556006** VCO module to generate RF signals in the **5.5–6.0 GHz** range.  
An **RP2040 microcontroller** drives the PLL over SPI, making it easy to test frequency sweeps, chirps, or single-tone synthesis.

## ✨ Features
- **ADF4158 PLL**
  - Fractional-N synthesizer  
  - Supports various shapes of ramps / chirps  

- **Innotion YSGM556006 VCO**
  - Very low cost VCO ($1.5/ea)
  - 5.5–6.0 GHz tuning range  
 
- **External (off-board) VCO Option**
  - SMA connectors expose VTUNE and VCO IN

- **RP2040 Controller**
  - Sends SPI commands for programming the PLL  
  - USB serial for sending commands / updating configs  

- **Other Board Components**
  - Loop filter for PLL stabilization  
  - Clean reference input stage (TCXO) 

## 📐 Purpose
This test board is designed for experimenting with PLL/VCO behavior at ~6 GHz.  
Typical use cases:

- Testing ADF4158 chirp/ramp features  
- Characterizing VCO tuning curve  
- LO generation for mixers or radar experiments  
- Measuring lock time, phase noise, loop stability  
- Learning / verifying SPI programming sequences for the ADF4158

## 🧠 How It Works
1. The **RP2040** boots and configures the ADF4158 via SPI.  
2. The ADF4158 sets the **divider ratio + ramp settings**.  
3. The loop filter drives the VCO’s **tuning voltage**, closing the PLL.  
4. The YSGM556006 outputs ~5.5–6 GHz RF.  
5. Lock status is monitored via **MUXOUT** exposed on the board.

## 🔌 SPI Interface (RP2040 → ADF4158)
- **MOSI** – PLL data input  
- **SCLK** – SPI clock  
- **LE** – Latch enable for register load  
- **MUXOUT** – Readable lock detect for debugging  

## ⚠️ Notes / Limitations
- The Innotion YSGM556006 is a very low cost ($1.5/ea) VCO, and has poor performance. This board was an attempt to test the feasibility of its use in a PLL.
- This test board is **not** a finalized RF product — it’s meant for bench characterization.  
- Ensure your RF chain and measurement equipment can safely handle 5–6 GHz at around 0 dBm.
