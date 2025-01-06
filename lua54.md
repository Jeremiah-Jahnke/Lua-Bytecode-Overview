
---

## Lua 5.4 Bytecode Breakdown

### Header Breakdown

This table provides a breakdown of the **Lua header** section in the bytecode format.

| Field                | Value                                    | Description                                                                          |
|----------------------|------------------------------------------|--------------------------------------------------------------------------------------|
| **Esc**              | `1b`                                     | Escape character                                                                     |
| **Signature**        | `4C 75 61`                               | Signature for Lua 5.4 (`"Lua"`)                                                      |
| **Version**          | `54`                                     | Lua version (in hexadecimal)                                                         |
| **Format**           | `00`                                     | Format version                                                                       |
| **Luac Data**        | `19 93 0D 0A 1A 0A`                      | Luac Data                                                                            |
| **Instruction Size** | `04`                                     | Size of each instruction in bytes                                                    |
| **Lua Integer Size** | `08`                                     | Size of Lua integers in bytes                                                        |
| **Lua Number Size**  | `08`                                     | Size of Lua floating-point numbers (double precision)                                |
| **Luac Int**         | `78 56 00 00 00 00 00 00`                | Lua integer (example: `0x00005678` in little-endian format)                          |
| **Luac Num**         | `00 00 00 00 00 28 77 40`                | Lua number in IEEE 754 double-precision floating-point format (370.5 in this case)   |

---

### Function Breakdown

This table breaks down the **function** section in the bytecode format.

| Field                   | Value                                    | Description                                                                    |
|-------------------------|------------------------------------------|--------------------------------------------------------------------------------|
| **Source**              | `0x40 0x74 0x65 0x73 0x74 0x2E 0x6C 0x75 0x61` | Source file (if available)                                                     |
| **Line Defined**        | `0x80`                                   | Line where the function is defined                                              |
| **Last Line Defined**   | `0x80`                                   | Last line where the function is defined                                         |
| **Num Parameters**      | `0x00`                                   | Number of parameters the function takes                                         |
| **Is Vararg**           | `0x01`                                   | Whether the function is a vararg (variable arguments)                           |
| **Max Stack Size**      | `0x02`                                   | Maximum stack size used by the function                                         |

---

### Code Section

The **bytecode instructions** for the function are provided here.

| Field                  | Value                                    | Description                                                                    |
|------------------------|------------------------------------------|--------------------------------------------------------------------------------|
| **Code Size**          | `0x85`                                   | Size of the bytecode instructions                                              |
| **Instructions**       | `0x51 0x00 0x00 0x00 0x0B 0x00 0x00 0x00 0x83 0x80 0x00 0x00 0x44 0x00 0x02 0x01 0x46 0x00 0x01 0x01` | The actual bytecode instructions                                                |

---

### Constants Section

This section breaks down the **constants** used by the function.

| Field                  | Value                                    | Description                                                                    |
|------------------------|------------------------------------------|--------------------------------------------------------------------------------|
| **Constants Count**    | `0x82`                                   | Number of constants used by the function                                        |
|
| **Constant Type**      | `0x04`                                   | Type of constant (string in this case)                                          |
| **String Size**        | `0x86`                                   | String Size                                                |
| **Constant Value**     | `0x70 0x72 0x69 0x6E 0x74`               | Constant string value: `"print"`                                         |
|
| **Constant Type**      | `0x04` | Type of constant (string in this case)                                          |
| **String Size**        | `0x8E` 								 | String Size                                                |
| **Constant Value**     | `0x48 0x65 0x6C 0x6C 0x6F 0x2C 0x20 0x57 0x6F 0x72 0x6C 0x64 0x21` | Constant string value: `"Hello, World!"`                                            |

---

### Upvalues Section

Details on the **upvalues** used by the function, which refer to variables from the outer scope.

| Field                  | Value                                    | Description                                                                    |
|------------------------|------------------------------------------|--------------------------------------------------------------------------------|
| **Upvalue Count**       | `0x81`                                   | Number of upvalues used                                                         |
| **Upvalue 0**           | `Instack: 0x01, Index: 0x00, Kind: 0x00`  | First upvalue details                                                           |

---

### Prototypes Section

This section details any **nested functions** (prototypes) within the function being dumped.

| Field                  | Value                                    | Description                                                                    |
|------------------------|------------------------------------------|--------------------------------------------------------------------------------|
| **Protos Count**        | `0x80`                                   | Number of prototypes (nested functions)                                         |

---

### Debug Information Section

This section contains **debug information** for the function, including line numbers and local variable names.

| Field                  | Value                                    | Description                                                                    |
|------------------------|------------------------------------------|--------------------------------------------------------------------------------|
| **Line Info Count**    | `0x85`                                   | Number of line numbers                                                          |
| **Line Info**          | `0x01 0x00 0x00 0x00 0x00`              | Line number information for the function                                        |
| **Absolute Line Info** | `0x80`              | Absolute line number information                                                |
| **Local Variables**    | `0x80`                                   | Number of local variables used                                                  |
| **Upvalue Names**      | `0x81`                                   | Number of upvalue names used                                                    |
| **Upvalue Name**       | `0x85`
| **Upvalue Name**       | `0x5F 0x45 0x4E 0x56`                    | Upvalue name: `"ENV"`                                                          |

---

## Example Hex Dump

### Header (31 Bytes):

```
1B 4C 75 61 54 00 19 93 0D 0A 1A 0A 04 08 08 78 56 
00 00 00 00 00 00 00 00 00 00 00 28 77 40
```

### Function (79 Bytes):

```
01 8A 40 74 65 73 74 2E 6C 75 61 80 80 00 01 02 85 
51 00 00 00 0B 00 00 00 83 80 00 00 44 00 02 01 46 
00 01 01 82 04 86 70 72 69 6E 74 04 8E 48 65 6C 6C 
6F 2C 20 57 6F 72 6C 64 21 81 01 00 00 80 85 01 00 
00 00 00 80 80 81 85 5F 45 4E 56
```

---