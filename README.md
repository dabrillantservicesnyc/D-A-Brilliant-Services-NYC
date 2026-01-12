# D-A-Brilliant-Services-NYC
<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Cotización - Servicio de Limusina</title>
  <link rel="stylesheet" href="estilos.css" />
</head>
<body>
  <main class="container">
    <h1>Solicitar cotización</h1>
    <p>Complete los datos para recibir un presupuesto rápido por email o WhatsApp.</p>

    <form id="quoteForm" action="/cotizar" method="post">
      <fieldset>
        <legend>Datos del viaje</legend>

        <label for="pickup">Lugar de recogida</label>
        <input id="pickup" name="pickup" type="text" required placeholder="Dirección o aeropuerto" />

        <label for="dropoff">Destino</label>
        <input id="dropoff" name="dropoff" type="text" required placeholder="Dirección o aeropuerto" />

        <label for="date">Fecha</label>
        <input id="date" name="date" type="date" required />

        <label for="time">Hora</label>
        <input id="time" name="time" type="time" required />

        <label for="passengers">Pasajeros</label>
        <input id="passengers" name="passengers" type="number" min="1" value="1" required />

        <label for="vehicle">Tipo de vehículo</label>
        <select id="vehicle" name="vehicle">
          <option value="sedan">Sedán (hasta 3 pax)</option>
          <option value="suv">SUV / Stretch (hasta 5 pax)</option>
          <option value="executive">Executive Van (hasta 8 pax)</option>
          <option value="limo">Limusina (hasta 10 pax)</option>
        </select>

        <label for="flight">Vuelo (opcional)</label>
        <input id="flight" name="flight" type="text" placeholder="Aerolínea y número de vuelo" />
      </fieldset>

      <fieldset>
        <legend>Extras / notas</legend>
        <label for="extras">Extras</label>
        <select id="extras" name="extras" multiple>
          <option value="meet_greet">Meet & Greet</option>
          <option value="child_seat">Silla para niño</option>
          <option value="waiting_time">Tiempo de espera adicional</option>
          <option value="bottled_water">Agua embotellada</option>
        </select>

        <label for="notes">Notas / instrucciones</label>
        <textarea id="notes" name="notes" rows="3" placeholder="Información adicional"></textarea>
      </fieldset>

      <fieldset>
        <legend>Contacto</legend>
        <label for="name">Nombre</label>
        <input id="name" name="name" type="text" required />

        <label for="phone">Teléfono</label>
        <input id="phone" name="phone" type="tel" required placeholder="+1 555 555 5555" />

        <label for="email">Email</label>
        <input id="email" name="email" type="email" required />
      </fieldset>

      <div class="actions">
        <button type="submit">Solicitar cotización</button>
        <button type="button" onclick="saveDraft()">Guardar borrador</button>
      </div>

      <p class="disclaimer">Al enviar, aceptas nuestros <a href="/terminos">Términos y Política de Privacidad</a>.</p>
    </form>
  </main>

  <script>
    // Pequeña mejora UX: guardar borrador en localStorage
    function saveDraft() {
      const data = Object.fromEntries(new FormData(document.getElementById('quoteForm')));
      localStorage.setItem('limoQuoteDraft', JSON.stringify(data));
      alert('Borrador guardado localmente.');
    }
    // Autocompletar borrador al cargar
    window.addEventListener('DOMContentLoaded', () => {
      const draft = localStorage.getItem('limoQuoteDraft');
      if (draft) {
        const obj = JSON.parse(draft);
        for (const [k,v] of Object.entries(obj)) {
          const el = document.querySelector(`[name="${k}"]`);
          if (el) el.value = v;
        }
      }
    });
  </script>
</body>
</html>
