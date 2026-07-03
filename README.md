# fluego-desktop-tauri-v2-win

**fluyo-cm2labs** — Registro de Trayectorias EAD. App desktop portable compilada con Tauri v2.

## 🔐 Seguridad: Encrypted Token Vault

Esta app incluye una bóveda de tokens cifrados integrada en el backend Rust:

| Característica | Detalle |
|---|---|
| Cifrado | AES-256-GCM |
| Clave | Generada en RAM al primer inicio |
| Persistencia de clave | Solo vive mientras la app está abierta |
| Almacenamiento | `%APPDATA%/com.cm2labs.fluyo/vault.enc` |
| Escritura | Atómica (temp + rename) — no corrompe en crash |
| Limpieza al cerrar | `clear_vault` se ejecuta automáticamente |

**Si la PC se reinicia o la app se cierra**, la clave AES se pierde y `vault.enc` queda ilegible. Los tokens solo están en texto plano en RAM mientras la app está activa.

### Comandos Tauri disponibles para el frontend
```javascript
await window.__TAURI__.invoke("store_token", { token: "..." })
await window.__TAURI__.invoke("get_token")     // devuelve string o null
await window.__TAURI__.invoke("clear_vault")
```

