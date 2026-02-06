<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Generador Recibos NRG</title>
    <style>
        /* Estilos de Interfaz */
        body { font-family: 'Arial', sans-serif; background-color: #f4f4f4; margin: 0; padding: 20px; }
        #ui-panel { 
            background: #fff; padding: 20px; border-radius: 8px; margin: 0 auto 20px; 
            max-width: 850px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); 
        }
        .input-row { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 15px; margin-bottom: 10px; }
        input, select, textarea { width: 100%; padding: 8px; border: 1px solid #ccc; border-radius: 4px; box-sizing: border-box; }
        button { background: #000; color: #fff; border: none; padding: 12px; cursor: pointer; width: 100%; font-weight: bold; border-radius: 4px; margin-top: 10px; }
        
        #print-area { display: flex; flex-direction: column; align-items: center; }

        /* Estructura del Recibo */
        .recibo-unit { 
            background: #fff; width: 21cm; height: 12.5cm; padding: 0.8cm 1.5cm; 
            margin-bottom: 0; border: 1px solid #eee; box-sizing: border-box; 
            position: relative; overflow: hidden;
        }

        /* Línea de recorte con tijeras */
        .recibo-unit:nth-child(odd):not(:last-child) {
            border-bottom: 2px dashed #aaa;
        }
        
        .recibo-unit:nth-child(odd):not(:last-child)::after {
            content: '✂-------------------------------------------------------------------------------------------------';
            position: absolute;
            bottom: -10px;
            left: 0;
            width: 100%;
            text-align: center;
            color: #aaa;
            font-size: 14px;
            letter-spacing: 2px;
        }

        /* Salto de página cada 2 unidades */
        .recibo-unit:nth-child(even) { page-break-after: always; }

        .header { width: 100%; margin-bottom: 10px; }
        .logo-box img { max-height: 75px; max-width: 210px; object-fit: contain; }
        .info-box { text-align: right; font-size: 9px; line-height: 1.1; color: #333; }
        
        .tabla-datos { width: 100%; border-collapse: collapse; }
        .tabla-datos td { padding: 6px 5px; border-bottom: 1px solid #eee; font-size: 13px; }
        .label { font-weight: bold; width: 30%; color: #000; }
        .valor { border-bottom: 1px solid #999; min-height: 16px; display: inline-block; width: 95%; text-transform: uppercase; }

        .firmas { margin-top: 35px; display: flex; justify-content: space-between; text-align: center; }
        .firma-linea { border-top: 1.5px solid #000; width: 45%; padding-top: 5px; font-size: 10px; font-weight: bold; }

        @media print {
            @page { margin: 0; }
            #ui-panel { display: none; }
            body { background: #fff; padding: 0; margin: 0; }
            .recibo-unit { border-left: none; border-right: none; border-top: none; }
        }
    </style>
</head>
<body>

<div id="ui-panel">
    <h3 style="margin-top:0;">Generador NRG - Web 24/7</h3>
    <div class="input-row">
        <div><label>Empresa:</label>
            <select id="emp" onchange="renderRecibos()">
                <option value="solar">NRG Solar</option>
                <option value="ing">NRG Ingeniería</option>
                <option value="mont">NRG Montajes & Maquinaria</option>
            </select>
        </div>
        <div><label>Copias:</label>
            <select id="cantidad" onchange="renderRecibos()">
                <option value="1">1 Recibo</option>
                <option value="2">2 Recibos (1 hoja)</option>
                <option value="4">4 Recibos (2 hojas)</option>
            </select>
        </div>
        <div><label>Fecha:</label><input type="text" id="iF" oninput="sync()"></div>
    </div>
    <div class="input-row">
        <div style="grid-column: span 2;"><label>Nombre Cliente:</label><input type="text" id="iN" oninput="sync()"></div>
        <div><label>Monto $ (Número):</label><input type="number" id="iM" step="0.01" oninput="convertirMonto(); sync();"></div>
    </div>
    <div style="margin-top:10px;">
        <label>Por concepto de:</label>
        <textarea id="iC" oninput="sync()" style="height: 40px;"></textarea>
    </div>
    <div style="margin-top:10px;">
        <label>Cantidad con Letra:</label>
        <input type="text" id="iL" oninput="sync()">
    </div>
    <button onclick="window.print()">IMPRIMIR RECIBOS</button>
</div>

<div id="print-area"></div>

<script>
    // AQUI SOLO PONEMOS LOS NOMBRES DE LOS ARCHIVOS QUE SUBIRAS A GITHUB
    const logos = {
        solar: 'solar.png',       // Asegúrate que tu archivo se llame así
        ing: 'ingenieria.png',    // Asegúrate que tu archivo se llame así
        mont: 'montajes.png'      // Asegúrate que tu archivo se llame así
    };

    const nombresEmpresa = {
        solar: 'NRG SOLAR. ',
        ing: 'NRG. ',
        mont: 'MONTAJES. '
    };

    function numeroALetras(num) {
        const unidades = ["", "UN", "DOS", "TRES", "CUATRO", "CINCO", "SEIS", "SIETE", "OCHO", "NUEVE"];
        const decenas = ["DIEZ", "ONCE", "DOCE", "TRECE", "CATORCE", "QUINCE", "DIECISEIS", "DIECISIETE", "DIECIOCHO", "DIECINUEVE"];
        const decenas_propias = ["", "", "VEINTE", "TREINTA", "CUARENTA", "CINCUENTA", "SESENTA", "SETENTA", "OCHENTA", "NOVENTA"];
        const centenas = ["", "CIENTO", "DOSCIENTOS", "TRESCIENTOS", "CUATROCIENTOS", "QUINIENTOS", "SEISCIENTOS", "SETENCIENTOS", "OCHOCIENTOS", "NOVECIENTOS"];

        function convertirGrupo(n) {
            let output = "";
            if (n === 100) return "CIEN ";
            if (n > 99) { output += centenas[Math.floor(n / 100)] + " "; n %= 100; }
            if (n > 19) { output += decenas_propias[Math.floor(n / 10)] + (n % 10 !== 0 ? " Y " : " "); n %= 10; }
            if (n > 9) { output += decenas[n - 10] + " "; n = 0; }
            if (n > 0) { output += unidades[n] + " "; }
            return output;
        }

        if (num === 0 || num === "") return "";
        let [entero, decimal] = parseFloat(num).toFixed(2).split('.');
        let nEntero = parseInt(entero);
        let letras = "";

        if (nEntero >= 1000000) {
            let millon = Math.floor(nEntero / 1000000);
            letras += (millon === 1 ? "UN MILLON " : convertirGrupo(millon) + " MILLONES ");
            nEntero %= 1000000;
        }
        if (nEntero >= 1000) {
            let mil = Math.floor(nEntero / 1000);
            letras += (mil === 1 ? "MIL " : convertirGrupo(mil) + " MIL ");
            nEntero %= 1000;
        }
        letras += convertirGrupo(nEntero);
        return `${letras}PESOS ${decimal}/100 M.N.`.replace(/\s+/g, ' ');
    }

    function convertirMonto() {
        const monto = document.getElementById('iM').value;
        if (monto) document.getElementById('iL').value = numeroALetras(monto);
    }

    function renderRecibos() {
        const cant = parseInt(document.getElementById('cantidad').value);
        const container = document.getElementById('print-area');
        const empValue = document.getElementById('emp').value;
        const etiquetaEmpresa = nombresEmpresa[empValue];
        
        container.innerHTML = ''; 

        for (let i = 0; i < cant; i++) {
            container.innerHTML += `
                <div class="recibo-unit">
                    <table class="header" width="100%">
                        <tr>
                            <td class="logo-box">
                                <div style="font-weight:bold; font-size:16px; margin-bottom:5px;">RECIBO DE PAGO</div>
                                <img src="${logos[empValue]}">
                            </td>
                            <td class="info-box">
                                <strong>${etiquetaEmpresa}NRG Ingeniería Electromecánica S.A. de C.V.</strong><br>
                                NIE1808155W9<br>
                                Calle Libramiento-Sur Poniente #376 Campestre Italiana CP. 76080<br>
                                Querétaro, Qro., Tel (442) 251 1682
                            </td>
                        </tr>
                    </table>
                    <table class="tabla-datos">
                        <tr><td class="label">Forma de pago:</td><td><span class="valor">De contado</span></td></tr>
                        <tr><td class="label">Fecha:</td><td><span class="valor oF"></span></td></tr>
                        <tr><td class="label">Nombre:</td><td><span class="valor oN"></span></td></tr>
                        <tr><td class="label">RFC del Cliente:</td><td><span class="valor">N/A</span></td></tr>
                        <tr><td class="label">Asesor Comercial:</td><td><span class="valor">N/A</span></td></tr>
                        <tr><td class="label">Se recibe la cantidad de:</td><td><span class="valor"><span class="oM"></span> (MXN)</span></td></tr>
                        <tr><td class="label">Por concepto de:</td><td><span class="valor oC"></span></td></tr>
                        <tr><td class="label">Cantidad con letra:</td><td><span class="valor oL"></span></td></tr>
                    </table>
                    <div class="firmas">
                        <div class="firma-linea">Nombre y firma de quien entrega</div>
                        <div class="firma-linea">Nombre y firma de quien recibe</div>
                    </div>
                </div>
            `;
        }
        sync(); 
    }

    function sync() {
        const fields = {
            'oF': document.getElementById('iF').value,
            'oN': document.getElementById('iN').value,
            'oM': document.getElementById('iM').value,
            'oC': document.getElementById('iC').value,
            'oL': document.getElementById('iL').value
        };
        for (let key in fields) {
            const elements = document.getElementsByClassName(key);
            for (let el of elements) el.innerText = fields[key];
        }
    }

    // Inicializar
    window.onload = renderRecibos;
</script>
</body>

</html>
