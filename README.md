# USLPForge Pro (v1.0.0)

### CCSDS 732.1-B-2 & ISO 21107 Unified Space Data Link Protocol (USLP) Studio

USLPForge Pro is an aerospace-grade developer studio, transfer frame synthesizer, packet multiplexer, COP-1 Go-Back-N / CLCW telemetry engine, CRC-16/CRC-32 error control field calculator, and 10-point normative compliance auditor built for spacecraft flight software engineers (NASA, ESA, JAXA, MBRSC UAE) and commercial space mission operators (Artemis lunar landers, Earth-observation CubeSats, Mars exploration orbiters).

---

## 🌟 Key Capabilities

- **Normative USLP Frame Synthesis (CCSDS 732.1-B-2)**: Generates bit-exact Transfer Frame Primary Headers (TFVN `0b1100`, SCID up to 16 bits, VCID up to 64 virtual channels, MAP ID 0..15, variable sequence length 0..7 octets).  
- **Flexible Frame Sizing (1 to 65,536 Octets)**: Full support for variable-length frames and high-throughput fixed-length frames with byte-accurate length tracking.  
- **Transfer Frame Data Field (TFDF) Multiplexing**: Implements Construction Rules `000` (Packet Stream with First Header Pointer `FHP`), `001` (Octet Stream), and `111` (Idle fill frames), multiplexing CCSDS Space Packets (CCSDS 133.0-B) and Encapsulation Packets (CCSDS 133.1-B).  
- **Operational Control Field (OCF) / CLCW Telemetry**: Generates 32-bit Command Link Control Words for COP-1 closed-loop retransmission tracking, FARM status, lockout reporting, and report value \$V(R)\$ synchronization.  
- **Dual Checksum Support (CRC-16 & CRC-32)**: Mathematical verification of CCITT CRC-16 (polynomial `0x1021`) and IEEE 802.3 CRC-32 (polynomial `0x04C11DB7`) Frame Error Control Fields (FECF).  
- **10-Point Normative Compliance Auditor**: Automated test and verification engine enforcing rules `USLP-001` through `USLP-010`.

---

## 📂 Project Structure

uslp-forge-pro/

├── source-code/

│   ├── uslp-engine.js           \# Core USLP encoder, decoder, CRC & CLCW engine

│   ├── uslp-auditor.js          \# 10-point normative compliance auditor

│   ├── uslp\_cli.py              \# Pure Python 3 CLI executable

│   ├── uslp-cli.py              \# Pure Python 3 CLI alias

│   ├── test\_runner.py          \# 10-suite unit test runner

│   └── index.html               \# Interactive Mission Control operations console

├── build/

│   └── uslp-forge-pro-v1.0.0.zip \# Standalone production bundle

├── documentation/

│   ├── CCSDS\_USLP\_SPECIFICATION.md \# Normative protocol specification

│   └── USLP\_COMPLIANCE\_MATRIX.md   \# 10-point requirement traceability

└── screenshots/

    ├── architecture-diagram.svg  \# System architecture diagram

    └── uslp-studio-preview.svg    \# Operations console preview

---

## 🚀 Quick Start

### Running Automated Tests

python3 source-code/test\_runner.py \-v

### Command Line Interface

\# Synthesize standard USLP Transfer Frame with Space Packet payload

python3 source-code/uslp\_cli.py \--mode frame \--scid 0x0042 \--vcid 1 \--seq 101 \--fecf CRC-16 \--ocf

\# Generate standalone CCSDS Space Packet

python3 source-code/uslp\_cli.py \--mode packet \--apid 0x01A0 \--seq 42 \--payload "TELEMETRY\_DATA"

\# Run 10-Point Normative Compliance Audit on synthesized frame

python3 source-code/uslp\_cli.py \--mode audit \--scid 0x0042 \--vcid 1 \--fecf CRC-16

\# Audit custom raw hexadecimal transfer frame

python3 source-code/uslp\_cli.py \--mode audit \--hex "C0 04 20 40 00 2C 0C 00 00 65 00 00 00 10 20 30 40 50 60"

### Launching the Web Operations Console

Open `source-code/index.html` in any modern web browser to access the interactive Mission Control dashboard, visual frame builder, bit-level hex dissector, and 10-point compliance scorecard.