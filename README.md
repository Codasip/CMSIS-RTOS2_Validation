# CMSIS-RTOS2 Validation

This repository contains a test suite that validates CMSIS-RTOS2 implementations. It uses [**Arm Virtual Hardware**](https://www.arm.com/virtual-hardware) to run a CI/CD flow to verify correct operation of the real-time operating systems (RTOS) under test on various Arm Cortex-M based processors.

**Arm Virtual Hardware** provides simulation models, software tooling, and infrastructure that can be integrated into CI/CD and MLOps development flows. The simulation models (called Arm Virtual Hardware Targets) are an implementation of a Cortex-M device sub-systems and are designed for complex software verification and testing. This allows simulation-based test automation of various software workloads, including unit tests, integration tests, and fault injection. Refer to the [Arm Virtual Hardware documentation](https://arm-software.github.io/AVH/main/overview/html/index.html) for more information.

## Repository structure

| Directory         | Contents                                                                          |
|-------------------|-----------------------------------------------------------------------------------|
| .github/workflows | Workflow YML files for running the test suite and for creating the documentation. |
| Doxygen           | Doxygen input files for creating the documentation.                               |
| Include           | Include files for test cases etc.                                                 |
| Layer             | Layers for creating the projects.                                                 |
| Project           | An example project that shows unit testing.                                       |
| Script            | Various shell scripts.                                                            |
| Source            | Test case source code.                                                            |

## Test matrix

Currently, the following tests are executed in the [CMSIS_RV2](./.github/workflows/cmsis_rv2.yml) workflow:

| RTOS     |  Device   | Compiler        |
|----------|-----------|-----------------|
| FreeRTOS |  ARMCM0P  | AC6, GCC, CLANG |
| FreeRTOS |  ARMCM3   | AC6, GCC, CLANG |
| FreeRTOS |  ARMCM4   | AC6, GCC, CLANG |
| FreeRTOS |  ARMCM7   | AC6, GCC, CLANG |
| FreeRTOS |  ARMCM23  | AC6, GCC, CLANG |
| FreeRTOS |  ARMCM33  | AC6, GCC, CLANG |
| FreeRTOS |  ARMCM55  | AC6, GCC, CLANG |
| FreeRTOS |  ARMCM85  | AC6, GCC, CLANG |
| RTX5     |  ARMCM0P  | AC6, GCC, CLANG |
| RTX5     |  ARMCM3   | AC6, GCC, CLANG |
| RTX5     |  ARMCM4   | AC6, GCC, CLANG |
| RTX5     |  ARMCM7   | AC6, GCC, CLANG |
| RTX5     |  ARMCM23  | AC6, GCC, CLANG |
| RTX5     |  ARMCM33  | AC6, GCC, CLANG |
| RTX5     |  ARMCM55  | AC6, GCC, CLANG |
| RTX5     |  ARMCM85  | AC6, GCC, CLANG |

## Codasip RISC-V Ports Validation

**Codasip** have ported RTX5 and CMSIS-FreeRTOS to RISC-V (32-bit) cores with the Codasip CLIC interrupt controller.

`RV2_Thread.c` has been modified to doubled the test stack size to 256 bytes for RISC-V as there are twice the number of register to save on the stack (31 for RISC-V, 16 for ARM).
There is also a minor fix for `TC_osThreadGetName_1()` to get it to pass with CMSIS-FreeRTOS.

The following RTOS/Platform combinations have been validated:

| RTOS     |  Device   | Compiler         | Tests Executed | Tests Passed | Notes  |
|----------|-----------|------------------|----------------|--------------|--------|
| FreeRTOS |  L110     | L110, GCC, CLANG |            139 |          136 |    [1] |
| RTX5     |  L110     | L110, GCC, CLANG |            161 |          161 |    [2] |

__Notes__

- [1] FreeRTOS is not fully compatible with CMSIS-RTOS2, so some tests are not executed and some fail, the RISC-V port validation suite test results are the same as for ARM, see: https://arm-software.github.io/CMSIS-FreeRTOS/v11.0.1/tech_data.html
- [2] All of the Validation Suite Tests pass.

## License

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
