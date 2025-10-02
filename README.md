# Baileys-AlwaysZakzz - WhatsApp Bot Framework 2025 Spesial Edition

<p align="center">
  <img src="https://img1.pixhost.to/images/9123/646717260_alwayszakzz.jpg" width="300" alt="Baileys AlwaysZakzz Logo" />
</p>

<p align="center">
  <a href="https://github.com/AlwaysZakzz/Baileys"><img src="https://img.shields.io/github/stars/AlwaysZakzz/Baileys?style=for-the-badge" alt="Stars"></a>
  <a href="https://www.npmjs.com/package/baileys-AlwaysZakzzr"><img src="https://img.shields.io/npm/v/@AlwaysZakzzr/baileys?style=for-the-badge" alt="NPM"></a>
</p>

---

**Baileys-AlwaysZakzzr** adalah versi modifikasi dari [WhiskeySockets/Baileys](https://github.com/WhiskeySockets/Baileys), dirancang khusus untuk para developer bot WhatsApp di tahun 2025. Fokus utama versi ini adalah kestabilan pairing code, session auto-recovery, dan fitur tambahan eksklusif yang tidak tersedia di versi original.

---

## Keunggulan Utama

- 🔒 **Pairing Kode Custom** — Pairing bot tanpa ribet dan full kendali
- 🔄 **Session Recovery Otomatis** — Tidak perlu login ulang setiap waktu
- 💡 **Support WhatsApp Business API** — Cocok untuk bot UMKM & bisnis besar
- ⚙️ **Modular & Siap Pakai** — Gampang diintegrasikan ke berbagai jenis bot
- 📱 **Multi-Device Compatible** — 100% jalan di WA MD versi terbaru
- 💬 **Dukungan Komunitas Developer** — Dari dev, untuk dev
- 💥 **Diuji Crash-Resistant** — Cocok untuk eksperimen bot tingkat lanjut



## Instalasi

```bash
npm install @AlwaysZakzzr/baileys

```
## Connecting

``` ts
import makeWASocket, { DisconnectReason } from '@AlwaysZakzzr/baileys'
import { Boom } from '@hapi/boom'

async function connectToWhatsApp () {
    const sock = makeWASocket({
        // can provide additional config here
        printQRInTerminal: true
    })
    sock.ev.on('connection.update', (update) => {
        const { connection, lastDisconnect } = update
        if(connection === 'close') {
            const shouldReconnect = (lastDisconnect.error as Boom)?.output?.statusCode !== DisconnectReason.loggedOut
            console.log('connection closed due to ', lastDisconnect.error, ', reconnecting ', shouldReconnect)
            // reconnect if not logged out
            if(shouldReconnect) {
                connectToWhatsApp()
            }
        } else if(connection === 'open') {
            console.log('opened connection')
        }
    })
    sock.ev.on('messages.upsert', m => {
        console.log(JSON.stringify(m, undefined, 2))

        console.log('replying to', m.messages[0].key.remoteJid)
        await sock.sendMessage(m.messages[0].key.remoteJid!, { text: 'Hello there!' })
    })
}
// run in main file
connectToWhatsApp()
``` 

## Thanks To All Developer

| Nama                | WhatsApp                                                                                                          |
| -------------------- | -------------------------------------------------------------------------------------------------------------------- |
| AlwaysZakzzr      | [6285719090171](https://wa.me/6285719090171) |
| Message Routes       | [message.route.js](https://github.com/salman0ansari/whatsapp-api-nodejs/blob/main/src/api/routes/message.route.js)   |
| Group Routes         | [group.route.js](https://github.com/salman0ansari/whatsapp-api-nodejs/blob/main/src/api/routes/group.route.js)       |
| Miscellaneous Routes | [misc.route.js](https://github.com/salman0ansari/whatsapp-api-nodejs/blob/main/src/api/routes/misc.route.js)         |

See all routes here [src/api/routes](https://github.com/salman0ansari/whatsapp-api-nodejs/tree/main/src/api/routes)
