# Marconi Barbershop

Website with client appointment scheduling + a barber’s dashboard, built using React, Vite, and Tailwind.

## Running locally

```bash
npm install
npm run dev
```

Opens in `http://localhost:5173`.

To generate the production version:

```bash
npm run build
npm run preview
```

## Structure

```
src/
  data/         catálogo de serviços, barbeiros e horário de funcionamento
  utils/        helpers de data/hora e a camada de persistência (storage.js)
  components/   Header, SiteView (site público), PanelView/Dashboard (painel)
  assets/images fotos reais da loja usadas na seção "Fotos"
```

## Barber's sign

The panel **has no visible link on the website**. To access it, add `#painel`
to the end of the address, for example:
```
https://yourdomain.com/#panel
```

After that, it asks for a password (defined in `src/components/PanelView.jsx`—currently `marconi2026`, for demonstration purposes only). Change this password, and before using it with real money, replace it with a proper login system; as it stands, this is merely a frontend-side lock, not actual authentication.

## ⚠️ Important Limitation: `localStorage`

Currently, appointments are saved using `localStorage`, which means they **only exist in the browser of the person who filled out the form**. If a client makes an appointment from their own mobile phone, it will not automatically appear on the barber’s dashboard on a different device.

While this is sufficient for testing the workflow, enabling the website and the dashboard to communicate across different devices would require a backend. The two functions that need to be updated are isolated in `src/utils/storage.js`—by replacing `getBookings`/`saveBookings` with `fetch` calls to an API (BarberHub already uses Node/Express + PostgreSQL via Prisma). The rest of the application would remain unchanged.

## Notifications for the Barber

The dashboard utilizes the browser's Notification API: with the tab open, it checks for new appointments every 15 seconds and triggers a notification. This works as long as the browser or application remains open (in most cases, even when running in the background), but it will not function if the application is completely closed. To support that, you would need actual push notifications (implemented via a service worker and a backend) or to leverage the WhatsApp integration—via the Meta Cloud API—which is already planned for BarberHub.

Qualquer host de site estático funciona (Vercel, Netlify, Cloudflare Pages):
build command `npm run build`, output directory `dist`.
