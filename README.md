# index.html
Gestión de Portabilidad Entel Chile
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Gestión de Portabilidad Entel Chile</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        /* Custom styles for rounded corners on elements */
        input, select, button, .rounded-lg, .rounded-xl, .bg-blue-50 {
            border-radius: 0.5rem; /* Equivalent to rounded-lg */
        }
        .rounded-xl {
            border-radius: 0.75rem; /* Equivalent to rounded-xl */
        }
        .shadow-md {
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }
        .shadow-lg {
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
        }
        .transition-transform {
            transition-property: transform;
            transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
            transition-duration: 150ms;
        }
        .hover\:scale-105:hover {
            transform: scale(1.05);
        }
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: .5; }
        }
        .animate-pulse {
            animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
        }
    </style>
</head>
<body class="min-h-screen bg-gradient-to-br from-blue-100 to-indigo-200 p-4 antialiased">
    <header class="bg-white shadow-md rounded-xl p-6 mb-8 text-center">
        <h1 class="text-4xl font-extrabold text-blue-800 mb-2">
            Gestión de Portabilidad Entel Chile
        </h1>
        <p class="text-lg text-gray-600 mb-4">
            Asigna y administra datos de portabilidad de manera eficiente.
        </p>
        <div class="text-sm text-gray-500">
            ID de Usuario: <span id="userIdDisplay" class="font-mono bg-blue-50 px-2 py-1 rounded-md">Cargando...</span>
        </div>
        <div id="messageDisplay" class="mt-4 p-3 bg-yellow-100 text-yellow-800 rounded-lg shadow-sm animate-pulse hidden"></div>
    </header>

    <section class="bg-white p-6 rounded-xl shadow-lg mb-8 max-w-2xl mx-auto">
        <h2 id="formTitle" class="text-2xl font-bold text-gray-800 mb-6">Registrar Nueva Portabilidad</h2>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <label class="block">
                <span class="text-gray-700 font-medium">Número de Teléfono (Principal):</span>
                <input type="text" id="numero" name="numero" placeholder="Ej: 912345678 (Opcional)"
                    class="mt-1 block w-full p-3 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500" />
            </label>
            <label class="block">
                <span class="text-gray-700 font-medium">RUT del Cliente:</span>
                <input type="text" id="rut" name="rut" placeholder="Ej: 12345678-9"
                    class="mt-1 block w-full p-3 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500" />
            </label>
            <label class="block col-span-1 md:col-span-2">
                <span class="text-gray-700 font-medium">Nombre Completo:</span>
                <input type="text" id="nombre" name="nombre" placeholder="Ej: Juan Pérez"
                    class="mt-1 block w-full p-3 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500" />
            </label>
            <label class="block">
                <span class="text-gray-700 font-medium">Operador Origen:</span>
                <select id="operadorOrigen" name="operadorOrigen"
                    class="mt-1 block w-full p-3 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500">
                    <option value="">Seleccionar...</option>
                    <option value="Claro">Claro</option>
                    <option value="Movistar">Movistar</option>
                    <option value="WOM">WOM</option>
                    <option value="VTR">VTR</option>
                    <option value="Virgin Mobile">Virgin Mobile</option>
                    <option value="Simple Móviles">Simple Móviles</option>
                    <option value="Gtd Móvil">Gtd Móvil</option>
                    <option value="Entel">Entel</option>
                    <option value="Otro">Otro</option>
                </select>
            </label>
            <label class="block">
                <span class="text-gray-700 font-medium">Fecha de Portabilidad:</span>
                <input type="date" id="fechaPortabilidad" name="fechaPortabilidad"
                    class="mt-1 block w-full p-3 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500" />
            </label>

            <label class="block col-span-1 md:col-span-2">
                <span class="text-gray-700 font-medium">Número de líneas a portar (1-29):</span>
                <input type="number" id="numLineas" name="numLineas" min="1" max="29" value="1"
                    class="mt-1 block w-full p-3 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500" />
                <p id="numLineasError" class="text-red-500 text-sm mt-1 hidden">Debe ingresar entre 1 y 29 líneas.</p>
            </label>

            <div id="phoneNumbersContainer" class="grid grid-cols-1 md:grid-cols-2 gap-4 col-span-full">
                </div>
            
            <label class="block col-span-1 md:col-span-2">
                <span class="text-gray-700 font-medium">Dirección del Cliente:</span>
                <input type="text" id="direccionCliente" name="direccionCliente" placeholder="Ej: Av. Providencia 1234, Providencia"
                    class="mt-1 block w-full p-3 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500" />
            </label>
            <label class="block col-span-1 md:col-span-2">
                <span class="text-gray-700 font-medium">Dirección de Entrega (Opcional):</span>
                <input type="text" id="direccionEntrega" name="direccionEntrega" placeholder="Ej: Calle Nueva 567, Depto. 101, Santiago Centro"
                    class="mt-1 block w-full p-3 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500" />
            </label>
            <label class="block col-span-1 md:col-span-2">
                <span class="text-gray-700 font-medium">Correo Electrónico:</span>
                <input type="email" id="correoElectronico" name="correoElectronico" placeholder="Ej: cliente@example.com"
                    class="mt-1 block w-full p-3 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500" />
            </label>
        </div>
        <button id="addUpdateBtn"
            class="mt-6 w-full bg-blue-600 hover:bg-blue-700 text-white font-bold py-3 px-6 rounded-lg shadow-md transition duration-300 ease-in-out transform hover:scale-105">
            Agregar Portabilidad
        </button>
        <button id="cancelEditBtn"
            class="mt-3 w-full bg-gray-400 hover:bg-gray-500 text-white font-bold py-3 px-6 rounded-lg shadow-md transition duration-300 ease-in-out transform hover:scale-105 hidden">
            Cancelar Edición
        </button>
    </section>

    <section class="bg-white p-6 rounded-xl shadow-lg max-w-4xl mx-auto">
        <h2 class="text-2xl font-bold text-gray-800 mb-6">Listado de Portabilidades Activas</h2>
        <div id="portabilitiesList" class="grid grid-cols-1 gap-4">
            <p class="text-gray-600 text-center py-8" id="noPortabilitiesMessage">
                No hay portabilidades registradas. ¡Agrega una nueva!
            </p>
        </div>
    </section>

    <footer class="mt-8 text-center text-gray-600 text-sm">
        <p>&copy; <span id="currentYear"></span> Sistema de Portabilidad Entel Chile. Desarrollado con React y Firebase.</p>
    </footer>

    <div id="messageModal" class="fixed inset-0 bg-gray-600 bg-opacity-50 flex items-center justify-center hidden z-50">
        <div class="bg-white p-8 rounded-xl shadow-lg max-w-xl w-full mx-4">
            <h3 class="text-xl font-bold text-gray-800 mb-4">Mensaje Generado</h3>
            <textarea id="generatedMessageTextarea" class="w-full h-64 p-3 border border-gray-300 rounded-lg resize-none mb-4" readonly></textarea>
            <div class="flex justify-end space-x-2">
                <button id="copyMessageBtn" class="bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out">Copiar Mensaje</button>
                <button id="closeModalBtn" class="bg-gray-400 hover:bg-gray-500 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out">Cerrar</button>
            </div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, addDoc, onSnapshot, doc, updateDoc, deleteDoc, query } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // Global variables provided by the Canvas environment
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        const firebaseConfig = JSON.parse(typeof __firebase_config !== 'undefined' ? __firebase_config : '{}');
        const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : '';

        let db;
        let auth;
        let currentUserId = '';
        let editingId = null; // Stores the ID of the portability being edited
        let currentPortabilitiesData = []; // Stores the latest fetched portability data
        let portingPhoneNumbers = []; // Array to store dynamically entered phone numbers

        const mockPlans = [
            'Sin asignar',
            'Plan Entel Lite 5GB',
            'Plan Entel Pro 15GB',
            'Plan Entel Ultra 30GB',
            'Plan Entel Ilimitado',
        ];

        // DOM Elements
        const userIdDisplay = document.getElementById('userIdDisplay');
        const messageDisplay = document.getElementById('messageDisplay');
        const formTitle = document.getElementById('formTitle');
        const numeroInput = document.getElementById('numero'); // Primary number input
        const rutInput = document.getElementById('rut');
        const nombreInput = document.getElementById('nombre');
        const operadorOrigenInput = document.getElementById('operadorOrigen');
        const fechaPortabilidadInput = document.getElementById('fechaPortabilidad');
        const numLineasInput = document.getElementById('numLineas'); // New input for number of lines
        const numLineasError = document.getElementById('numLineasError'); // Error for numLineas
        const phoneNumbersContainer = document.getElementById('phoneNumbersContainer'); // Container for dynamic inputs
        const direccionClienteInput = document.getElementById('direccionCliente');
        const direccionEntregaInput = document.getElementById('direccionEntrega');
        const correoElectronicoInput = document.getElementById('correoElectronico');
        const addUpdateBtn = document.getElementById('addUpdateBtn');
        const cancelEditBtn = document.getElementById('cancelEditBtn');
        const portabilitiesList = document.getElementById('portabilitiesList');
        const noPortabilitiesMessage = document.getElementById('noPortabilitiesMessage');

        // Message Modal Elements
        const messageModal = document.getElementById('messageModal');
        const generatedMessageTextarea = document.getElementById('generatedMessageTextarea');
        const copyMessageBtn = document.getElementById('copyMessageBtn');
        const closeModalBtn = document.getElementById('closeModalBtn');


        // Function to display messages to the user
        function showMessage(msg, duration = 3000) {
            messageDisplay.textContent = msg;
            messageDisplay.classList.remove('hidden');
            setTimeout(() => {
                messageDisplay.classList.add('hidden');
                messageDisplay.textContent = '';
            }, duration);
        }

        // Initialize Firebase and Auth
        async function initializeFirebase() {
            try {
                const app = initializeApp(firebaseConfig);
                db = getFirestore(app);
                auth = getAuth(app);

                onAuthStateChanged(auth, async (user) => {
                    if (user) {
                        console.log("Firebase Auth State Changed: User is signed in.", user.uid);
                        currentUserId = user.uid;
                        userIdDisplay.textContent = currentUserId;
                        setupRealtimeListener();
                    } else {
                        console.log("Firebase Auth State Changed: No user is signed in. Attempting sign-in...");
                        try {
                            if (initialAuthToken) {
                                await signInWithCustomToken(auth, initialAuthToken);
                                console.log("Signed in with custom token.");
                            } else {
                                await signInAnonymously(auth);
                                console.log("Signed in anonymously.");
                            }
                        } catch (error) {
                            console.error("Error signing in:", error);
                            showMessage(`Error al iniciar sesión: ${error.message}`);
                        }
                    }
                });
            } catch (error) {
                console.error("Error initializing Firebase:", error);
                showMessage(`Error al inicializar Firebase: ${error.message}`);
            }
        }

        // Set up real-time listener for portabilities
        function setupRealtimeListener() {
            if (!db || !currentUserId) {
                return;
            }
            const portabilitiesCollectionRef = collection(db, `artifacts/${appId}/public/data/entelPortabilities`);
            const q = query(portabilitiesCollectionRef);

            onSnapshot(q, (snapshot) => {
                const data = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
                // Sort data in memory if needed
                data.sort((a, b) => new Date(b.fechaPortabilidad) - new Date(a.fechaPortabilidad));
                currentPortabilitiesData = data; // Update global data
                renderPortabilities(data);
            }, (error) => {
                console.error("Error fetching portabilities:", error);
                showMessage(`Error al cargar portabilidades: ${error.message}`);
            });
        }

        // Render portabilities to the DOM
        function renderPortabilities(portabilities) {
            portabilitiesList.innerHTML = ''; // Clear existing list
            if (portabilities.length === 0) {
                noPortabilitiesMessage.classList.remove('hidden');
                portabilitiesList.appendChild(noPortabilitiesMessage);
            } else {
                noPortabilitiesMessage.classList.add('hidden');
                portabilities.forEach(p => {
                    const portabilityItem = document.createElement('div');
                    portabilityItem.className = 'bg-blue-50 border border-blue-200 rounded-lg p-5 shadow-sm flex flex-col sm:flex-row justify-between items-start sm:items-center space-y-4 sm:space-y-0 sm:space-x-4';

                    const lineasHtml = p.lineasPortar && p.lineasPortar.length > 0
                        ? `<p class="text-sm text-gray-700">Líneas a portar: <span class="font-medium">${p.lineasPortar.join(', ')}</span></p>`
                        : (p.numero ? `<p class="text-sm text-gray-700">Teléfono: <span class="font-medium">${p.numero}</span></p>` : '');


                    portabilityItem.innerHTML = `
                        <div class="flex-grow">
                            <p class="text-lg font-semibold text-blue-800">${p.nombre}</p>
                            ${lineasHtml}
                            <p class="text-sm text-gray-700">RUT: <span class="font-medium">${p.rut}</span></p>
                            <p class="text-sm text-gray-700">Origen: <span class="font-medium">${p.operadorOrigen}</span></p>
                            <p class="text-sm text-gray-700">Fecha Port.: <span class="font-medium">${p.fechaPortabilidad}</span></p>
                            <p class="text-sm text-gray-700">Dirección Cliente: <span class="font-medium">${p.direccionCliente || 'N/A'}</span></p>
                            <p class="text-sm text-gray-700">Dirección Entrega: <span class="font-medium">${p.direccionEntrega || 'N/A'}</span></p>
                            <p class="text-sm text-gray-700">Correo Electrónico: <span class="font-medium">${p.correoElectronico || 'N/A'}</span></p>
                            <p class="text-md text-blue-700 font-bold mt-1">
                                Plan Asignado: <span class="text-blue-900">${p.planAsignado}</span>
                            </p>
                        </div>
                        <div class="flex flex-col space-y-2 w-full sm:w-auto">
                            <button data-id="${p.id}" data-plan="${p.planAsignado}" class="assign-plan-btn bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out flex items-center justify-center transform hover:scale-105">
                                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fillRule="evenodd" d="M3 3a1 1 0 000 2v8a2 2 0 002 2h2.586l1.293 1.293a1 1 0 001.414 0L12.414 15H15a2 2 0 002-2V5a1 1 0 00-1-1h-4.586l-1.293-1.293a1 1 0 00-1.414 0L7.586 4H3zm13 9V5H4v7h12z" clipRule="evenodd"></path></svg>
                                Asignar Siguiente Plan
                            </button>
                            <button data-id="${p.id}" class="edit-btn bg-yellow-500 hover:bg-yellow-600 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out flex items-center justify-center transform hover:scale-105">
                                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M13.586 3.586a2 2 0 112.828 2.828L15.414 10H17a1 1 0 110 2h-1v1a1 1 0 11-2 0v-1h-1a1 1 0 110-2h1.586l-4.293-4.293zM10 13a1 1 0 00-1 1v1a1 1 0 001 1h1a1 1 0 001-1v-1a1 1 0 00-1-1h-1zM5 10a1 1 0 00-1 1v4a1 1 0 001 1h5a1 1 0 001-1v-4a1 1 0 00-1-1H5z"></path></svg>
                                Editar
                            </button>
                            <button data-id="${p.id}" class="delete-btn bg-red-500 hover:bg-red-600 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out flex items-center justify-center transform hover:scale-105">
                                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fillRule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm6 0a1 1 0 01-2 0v6a1 1 0 112 0V8z" clipRule="evenodd"></path></svg>
                                Eliminar
                            </button>
                            <button data-id="${p.id}" class="generate-message-btn bg-purple-500 hover:bg-purple-600 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out flex items-center justify-center transform hover:scale-105">
                                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M2 5a2 2 0 012-2h12a2 2 0 012 2v10a2 2 0 01-2 2H4a2 2 0 01-2-2V5zm10.5 1h-5a.5.5 0 00-.5.5v3a.5.5 0 00.5.5h5a.5.5 0 00.5-.5v-3a.5.5 0 00-.5-.5zM7 14a1 1 0 100 2h6a1 1 0 100-2H7z"></path></svg>
                                Generar Mensaje
                            </button>
                            <button data-id="${p.id}" class="verify-giro-btn bg-indigo-500 hover:bg-indigo-600 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out flex items-center justify-center transform hover:scale-105">
                                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fillRule="evenodd" d="M10 2a1 1 0 00-1 1v1a1 1 0 001 1h4a1 1 0 001-1V3a1 1 0 00-1-1h-4zm0 6a1 1 0 00-1 1v7a1 1 0 001 1h4a1 1 0 001-1V9a1 1 0 00-1-1h-4z" clipRule="evenodd"></path></svg>
                                VERIFICAR GIRO COMERCIAL
                            </button>
                            <button data-id="${p.id}" class="check-debt-entel-btn bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out flex items-center justify-center transform hover:scale-105">
                                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fillRule="evenodd" d="M4 4a2 2 0 00-2 2v8a2 2 0 002 2h12a2 2 0 002-2V6a2 2 0 00-2-2H4zm0 2h12v8H4V6zm-2 3a2 2 0 012-2h12a2 2 0 012 2v4a2 2 0 01-2 2H4a2 2 0 01-2-2V9z" clipRule="evenodd"></path></svg>
                                DEUDA ENTEL NO CASTIGADA
                            </button>
                            <button data-id="${p.id}" class="check-debt-wom-btn bg-pink-600 hover:bg-pink-700 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out flex items-center justify-contrast flex items-center justify-center transform hover:scale-105">
                                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fillRule="evenodd" d="M4 4a2 2 0 00-2 2v8a2 2 0 002 2h12a2 2 0 002-2V6a2 2 0 00-2-2H4zm0 2h12v8H4V6zm-2 3a2 2 0 012-2h12a2 2 0 012 2v4a2 2 0 01-2 2H4a2 2 0 01-2-2V9z" clipRule="evenodd"></path></svg>
                                CONSULTA BOLETAS VENCIDAS EN WOM
                            </button>
                            <button data-id="${p.id}" class="check-coverage-btn bg-blue-500 hover:bg-blue-600 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out flex items-center justify-center transform hover:scale-105">
                                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fillRule="evenodd" d="M4 3a2 2 0 00-2 2v10a2 2 0 002 2h12a2 2 0 002-2V5a2 2 0 00-2-2H4zm0 2h12v.5H4V5zM4 9h12v.5H4V9zm0 4h12v.5H4V13z" clipRule="evenodd"></path></svg>
                                COBERTURA DE ENTEL
                            </button>
                            <button data-id="${p.id}" class="check-churn-debt-btn bg-gray-700 hover:bg-gray-800 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out flex items-center justify-center transform hover:scale-105">
                                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fillRule="evenodd" d="M4 4a2 2 0 00-2 2v8a2 2 0 002 2h12a2 2 0 002-2V6a2 2 0 00-2-2H4zm0 2h12v8H4V6zm-2 3a2 2 0 012-2h12a2 2 0 012 2v4a2 2 0 01-2 2H4a2 2 0 01-2-2V9z" clipRule="evenodd"></path></svg>
                                DEUDA CHURN
                            </button>
                            <button data-id="${p.id}" class="check-crm-btn bg-teal-500 hover:bg-teal-600 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out flex items-center justify-center transform hover:scale-105">
                                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fillRule="evenodd" d="M7 2a2 2 0 00-2 2v12a2 2 0 002 2h6a2 2 0 002-2V4a2 2 0 00-2-2H7zm0 2h6v8H7V4zm0 10a1 1 0 100 2h6a1 1 0 100-2H7z" clipRule="evenodd"></path></svg>
                                CRM DE VENTAS
                            </button>
                        </div>
                    `;
                    portabilitiesList.appendChild(portabilityItem);
                });

                // Attach event listeners to the newly rendered buttons
                document.querySelectorAll('.assign-plan-btn').forEach(button => {
                    button.addEventListener('click', (e) => {
                        const id = e.currentTarget.dataset.id;
                        const currentPlan = e.currentTarget.dataset.plan;
                        handleAssignPlan(id, currentPlan);
                    });
                });

                document.querySelectorAll('.edit-btn').forEach(button => {
                    button.addEventListener('click', (e) => {
                        const id = e.currentTarget.dataset.id;
                        const portability = currentPortabilitiesData.find(p => p.id === id);
                        if (portability) {
                            handleEditPortability(portability);
                        }
                    });
                });

                document.querySelectorAll('.delete-btn').forEach(button => {
                    button.addEventListener('click', (e) => {
                        const id = e.currentTarget.dataset.id;
                        handleDeletePortability(id);
                    });
                });

                document.querySelectorAll('.generate-message-btn').forEach(button => {
                    button.addEventListener('click', (e) => {
                        const id = e.currentTarget.dataset.id;
                        const portability = currentPortabilitiesData.find(p => p.id === id);
                        if (portability) {
                            handleGenerateMessage(portability);
                        }
                    });
                });

                document.querySelectorAll('.verify-giro-btn').forEach(button => {
                    button.addEventListener('click', () => {
                        window.open('https://zeus.sii.cl/cvc/stc/stc.html', '_blank');
                    });
                });

                document.querySelectorAll('.check-debt-entel-btn').forEach(button => {
                    button.addEventListener('click', () => {
                        window.open('https://miperfil.entel.cl/CL_Web_Unified_Payment_EU/Detalle_Deuda.aspx', '_blank');
                    });
                });

                document.querySelectorAll('.check-debt-wom-btn').forEach(button => {
                    button.addEventListener('click', () => {
                        window.open('https://pagofacilwom.cl/pago_facil/pagarCuenta?U2FsdGVkX19sXMxmuAc8uSmG8SNxVI/pPfz0/G6rre4qpYr2rGvO3QHAhSpIA9DDW9pOQ/rF7/WVs4HUQArCBg', '_blank');
                    });
                });

                document.querySelectorAll('.check-coverage-btn').forEach(button => {
                    button.addEventListener('click', () => {
                        window.open('https://www.entel.cl/landing/cobertura/movil/', '_blank');
                    });
                });

                document.querySelectorAll('.check-churn-debt-btn').forEach(button => {
                    button.addEventListener('click', () => {
                        window.open('https://docs.google.com/spreadsheets/d/1_j33eMDEQUuVTDKsLGD4cio-6Bho5fz2z5bTmn9kqAg/edit?gid=1154631292#gid=1154631292', '_blank');
                    });
                });

                document.querySelectorAll('.check-crm-btn').forEach(button => { // New button event listener
                    button.addEventListener('click', () => {
                        window.open('https://master.smartcrm.cl/gestion/home.html', '_blank');
                    });
                });
            }
        }

        // Function to render dynamic phone number input fields
        function renderPhoneNumberInputs(count) {
            phoneNumbersContainer.innerHTML = ''; // Clear previous inputs
            portingPhoneNumbers = Array(count).fill(''); // Reset array based on new count

            for (let i = 0; i < count; i++) {
                const div = document.createElement('div');
                div.className = 'col-span-1';
                div.innerHTML = `
                    <label class="block">
                        <span class="text-gray-700 font-medium">Línea a portar ${i + 1}:</span>
                        <input type="text" id="portingNumber_${i}" name="portingNumber_${i}"
                            placeholder="Ej: 912345678"
                            class="mt-1 block w-full p-3 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500" />
                        <p id="portingNumberError_${i}" class="text-red-500 text-sm mt-1 hidden"></p>
                    </label>
                `;
                phoneNumbersContainer.appendChild(div);

                const input = document.getElementById(`portingNumber_${i}`);
                input.addEventListener('input', (e) => {
                    portingPhoneNumbers[i] = e.target.value;
                    validateSinglePhoneNumber(e.target);
                });
            }
            // Re-validate existing numbers if they were loaded (e.g., during edit)
            portingPhoneNumbers.forEach((num, index) => {
                const input = document.getElementById(`portingNumber_${index}`);
                if (input && num) { // Check if input exists and has a value to validate
                    input.value = num; // Set value if it exists in the global array
                    validateSinglePhoneNumber(input);
                }
            });
        }

        // Function to validate a single phone number input
        function validateSinglePhoneNumber(inputElement) {
            const errorDisplay = document.getElementById(`portingNumberError_${inputElement.id.split('_')[1]}`);
            const value = inputElement.value.trim();
            
            if (value.length > 0 && value.length !== 9) {
                errorDisplay.textContent = 'El número debe tener exactamente 9 dígitos.';
                errorDisplay.classList.remove('hidden');
                inputElement.classList.add('border-red-500');
                inputElement.classList.remove('focus:border-blue-500');
                return false;
            } else {
                errorDisplay.classList.add('hidden');
                errorDisplay.textContent = '';
                inputElement.classList.remove('border-red-500');
                inputElement.classList.add('focus:border-blue-500');
                return true;
            }
        }

        // Handle adding or updating a portability
        async function handleAddUpdatePortability(e) {
            e.preventDefault();

            // Form validation
            let isValid = true;

            const rut = rutInput.value.trim();
            if (!rut) {
                showMessage('El RUT del cliente es obligatorio.', 3000);
                isValid = false;
            }

            const nombre = nombreInput.value.trim();
            if (!nombre) {
                showMessage('El nombre completo es obligatorio.', 3000);
                isValid = false;
            }

            const operadorOrigen = operadorOrigenInput.value;
            if (!operadorOrigen) {
                showMessage('El operador de origen es obligatorio.', 3000);
                isValid = false;
            }

            const fechaPortabilidad = fechaPortabilidadInput.value;
            if (!fechaPortabilidad) {
                showMessage('La fecha de portabilidad es obligatoria.', 3000);
                isValid = false;
            }

            const numLineas = parseInt(numLineasInput.value);
            if (isNaN(numLineas) || numLineas < 1 || numLineas > 29) {
                numLineasError.classList.remove('hidden');
                isValid = false;
            } else {
                numLineasError.classList.add('hidden');
            }

            // Validate all dynamically added phone numbers
            const validPortingNumbers = [];
            let allPortingNumbersValid = true;
            for (let i = 0; i < numLineas; i++) {
                const input = document.getElementById(`portingNumber_${i}`);
                if (input) {
                    if (!validateSinglePhoneNumber(input)) {
                        allPortingNumbersValid = false;
                    }
                    if (input.value.trim()) { // Only add non-empty numbers
                        validPortingNumbers.push(input.value.trim());
                    }
                }
            }
            if (!allPortingNumbersValid) {
                isValid = false;
                showMessage('Por favor, corrige los números de teléfono inválidos.', 3000);
            }
            if (numLineas > 0 && validPortingNumbers.length === 0) {
                 showMessage('Debe ingresar al menos un número de teléfono a portar.', 3000);
                 isValid = false;
            }
            if (validPortingNumbers.length !== numLineas) {
                showMessage(`Debe ingresar ${numLineas} números de teléfono, o asegúrese que todos los campos de números estén llenos y válidos.`, 5000);
                isValid = false;
            }


            if (!isValid) {
                return;
            }

            const portabilityData = {
                rut: rut,
                nombre: nombre,
                operadorOrigen: operadorOrigen,
                fechaPortabilidad: fechaPortabilidad,
                numLineas: numLineas,
                lineasPortar: validPortingNumbers, // Store all dynamically entered numbers
                numero: numeroInput.value.trim(), // Primary number, if entered
                direccionCliente: direccionClienteInput.value.trim(),
                direccionEntrega: direccionEntregaInput.value.trim(),
                correoElectronico: correoElectronicoInput.value.trim(),
                planAsignado: 'Sin asignar', // Default value
                userId: currentUserId, // Store the user who added/edited this
                timestamp: new Date().toISOString(), // Add timestamp
            };

            try {
                if (editingId) {
                    // Update existing portability
                    const docRef = doc(db, `artifacts/${appId}/public/data/entelPortabilities`, editingId);
                    await updateDoc(docRef, portabilityData);
                    showMessage('Portabilidad actualizada exitosamente!');
                } else {
                    // Add new portability
                    await addDoc(collection(db, `artifacts/${appId}/public/data/entelPortabilities`), portabilityData);
                    showMessage('Portabilidad agregada exitosamente!');
                }
                resetForm();
            } catch (error) {
                console.error("Error adding/updating document: ", error);
                showMessage(`Error al guardar portabilidad: ${error.message}`);
            }
        }

        // Handle assigning the next plan
        async function handleAssignPlan(id, currentPlan) {
            const currentIndex = mockPlans.indexOf(currentPlan);
            const nextIndex = (currentIndex + 1) % mockPlans.length;
            const nextPlan = mockPlans[nextIndex];

            try {
                const docRef = doc(db, `artifacts/${appId}/public/data/entelPortabilities`, id);
                await updateDoc(docRef, { planAsignado: nextPlan });
                showMessage(`Plan actualizado a: ${nextPlan}`);
            } catch (error) {
                console.error("Error updating plan:", error);
                showMessage(`Error al asignar plan: ${error.message}`);
            }
        }

        // Handle editing a portability
        function handleEditPortability(portability) {
            editingId = portability.id;
            formTitle.textContent = 'Editar Portabilidad';
            addUpdateBtn.textContent = 'Actualizar Portabilidad';
            cancelEditBtn.classList.remove('hidden');

            numeroInput.value = portability.numero || '';
            rutInput.value = portability.rut || '';
            nombreInput.value = portability.nombre || '';
            operadorOrigenInput.value = portability.operadorOrigen || '';
            fechaPortabilidadInput.value = portability.fechaPortabilidad || '';
            numLineasInput.value = portability.numLineas || 1;
            direccionClienteInput.value = portability.direccionCliente || '';
            direccionEntregaInput.value = portability.direccionEntrega || '';
            correoElectronicoInput.value = portability.correoElectronico || '';

            // Populate dynamic phone number inputs if they exist
            portingPhoneNumbers = portability.lineasPortar || [];
            renderPhoneNumberInputs(portability.numLineas || 1); // Re-render inputs based on saved count

            // Scroll to the form
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // Handle deleting a portability
        async function handleDeletePortability(id) {
            if (confirm('¿Estás seguro de que quieres eliminar esta portabilidad?')) {
                try {
                    await deleteDoc(doc(db, `artifacts/${appId}/public/data/entelPortabilities`, id));
                    showMessage('Portabilidad eliminada exitosamente.');
                } catch (error) {
                    console.error("Error removing document: ", error);
                    showMessage(`Error al eliminar portabilidad: ${error.message}`);
                }
            }
        }

        // Handle generating and displaying the message
        function handleGenerateMessage(portability) {
            const { nombre, rut, numero, lineasPortar, operadorOrigen, fechaPortabilidad, planAsignado, direccionCliente, direccionEntrega, correoElectronico } = portability;
            
            let phoneNumbersList = '';
            if (lineasPortar && lineasPortar.length > 0) {
                phoneNumbersList = `Números a portar: ${lineasPortar.join(', ')}\n`;
            } else if (numero) {
                phoneNumbersList = `Número principal: ${numero}\n`;
            }

            const message = `
PORTABILIDAD ENTEL - CHILE

Datos del Cliente:
Nombre: ${nombre}
RUT: ${rut}
${phoneNumbersList}Operador Origen: ${operadorOrigen}
Fecha de Portabilidad: ${fechaPortabilidad}
Plan Asignado: ${planAsignado}
Dirección Cliente: ${direccionCliente || 'No especificada'}
Dirección de Entrega: ${direccionEntrega || 'No especificada'}
Correo Electrónico: ${correoElectronico || 'No especificado'}

¡Éxito en la gestión!
            `.trim();
            generatedMessageTextarea.value = message;
            messageModal.classList.remove('hidden');
        }

        // Reset form to initial state
        function resetForm() {
            editingId = null;
            formTitle.textContent = 'Registrar Nueva Portabilidad';
            addUpdateBtn.textContent = 'Agregar Portabilidad';
            cancelEditBtn.classList.add('hidden');

            numeroInput.value = '';
            rutInput.value = '';
            nombreInput.value = '';
            operadorOrigenInput.value = '';
            fechaPortabilidadInput.value = '';
            numLineasInput.value = 1;
            direccionClienteInput.value = '';
            direccionEntregaInput.value = '';
            correoElectronicoInput.value = '';
            
            // Clear and reset dynamic phone number inputs
            portingPhoneNumbers = [];
            renderPhoneNumberInputs(1); // Render one empty input by default
            numLineasError.classList.add('hidden'); // Hide any error
        }

        // Event Listeners
        addUpdateBtn.addEventListener('click', handleAddUpdatePortability);
        cancelEditBtn.addEventListener('click', resetForm);
        closeModalBtn.addEventListener('click', () => messageModal.classList.add('hidden'));
        copyMessageBtn.addEventListener('click', () => {
            generatedMessageTextarea.select();
            document.execCommand('copy');
            showMessage('Mensaje copiado al portapapeles.', 2000);
        });

        // Event listener for numLineas input to dynamically render phone number inputs
        numLineasInput.addEventListener('input', () => {
            const count = parseInt(numLineasInput.value);
            if (!isNaN(count) && count >= 1 && count <= 29) {
                renderPhoneNumberInputs(count);
                numLineasError.classList.add('hidden');
            } else {
                numLineasError.classList.remove('hidden');
                phoneNumbersContainer.innerHTML = ''; // Clear inputs if invalid
            }
        });

        // Initial setup
        document.addEventListener('DOMContentLoaded', () => {
            document.getElementById('currentYear').textContent = new Date().getFullYear();
            initializeFirebase();
            renderPhoneNumberInputs(1); // Render one phone number input on load
        });

    </script>
</body>
</html>
