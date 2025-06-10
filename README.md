# index.html
Gestión de Portabilidad Entel Chile
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Gestión de Portabilidad Entel Chile</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Google Fonts - Inter -->
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
        /* Custom scrollbar for pricing modal content */
        .modal-content-scrollable::-webkit-scrollbar {
            width: 8px;
        }
        .modal-content-scrollable::-webkit-scrollbar-track {
            background: #f1f1f1;
            border-radius: 10px;
        }
        .modal-content-scrollable::-webkit-scrollbar-thumb {
            background: #888;
            border-radius: 10px;
        }
        .modal-content-scrollable::-webkit-scrollbar-thumb:hover {
            background: #555;
        }
    </style>
</head>
<body class="min-h-screen bg-gradient-to-br from-blue-100 to-indigo-200 p-4 antialiased">
    <!-- Header and User ID -->
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

    <!-- Add/Edit Portability Form -->
    <section class="bg-white p-6 rounded-xl shadow-lg mb-8 max-w-2xl mx-auto">
        <h2 id="formTitle" class="text-2xl font-bold text-gray-800 mb-6">Registrar Nueva Portabilidad</h2>
        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
            <!-- Número de teléfono (primary, optional if multiple lines) -->
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

            <!-- Número de líneas a portar -->
            <label class="block col-span-1 md:col-span-2">
                <span class="text-gray-700 font-medium">Número de líneas a portar (1-29):</span>
                <input type="number" id="numLineas" name="numLineas" min="1" max="29" value="1"
                    class="mt-1 block w-full p-3 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500" />
                <p id="numLineasError" class="text-red-500 text-sm mt-1 hidden">Debe ingresar entre 1 y 29 líneas.</p>
            </label>

            <!-- Dynamic phone number inputs container -->
            <div id="phoneNumbersContainer" class="grid grid-cols-1 md:grid-cols-2 gap-4 col-span-full">
                <!-- Dynamic phone number inputs will be inserted here by JavaScript -->
            </div>
            
            <label class="block col-span-1 md:col-span-2">
                <span class="text-gray-700 font-medium">Dirección del Cliente:</span>
                <input type="text" id="direccionCliente" name="direccionCliente" placeholder="Ej: Av. Providencia 1234, Providencia"
                    class="mt-1 block w-full p-3 border border-gray-300 rounded-lg shadow-sm focus:ring-blue-500 focus:border-blue-500" />
            </label>
            <!-- Checkbox for same delivery address -->
            <div class="block col-span-1 md:col-span-2">
                <label class="inline-flex items-center mt-2">
                    <input type="checkbox" id="sameAddressCheckbox" class="form-checkbox h-5 w-5 text-blue-600">
                    <span class="ml-2 text-gray-700 text-sm">Usar la misma dirección para la entrega del chip (24 a 72 horas)</span>
                </label>
            </div>
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

    <!-- Portability List -->
    <section class="bg-white p-6 rounded-xl shadow-lg max-w-4xl mx-auto">
        <h2 class="text-2xl font-bold text-gray-800 mb-6">Listado de Portabilidades Activas</h2>
        <div id="portabilitiesList" class="grid grid-cols-1 gap-4">
            <p class="text-gray-600 text-center py-8" id="noPortabilitiesMessage">
                No hay portabilidades registradas. ¡Agrega una nueva!
            </p>
        </div>
    </section>

    <!-- Footer -->
    <footer class="mt-8 text-center text-gray-600 text-sm">
        <p>&copy; <span id="currentYear"></span> Sistema de Portabilidad Entel Chile. Desarrollado con React y Firebase.</p>
    </footer>

    <!-- Message Modal -->
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

    <!-- Pricing Modal -->
    <div id="pricingModal" class="fixed inset-0 bg-gray-600 bg-opacity-50 flex items-center justify-center hidden z-50">
        <div class="bg-white p-8 rounded-xl shadow-lg max-w-3xl w-full mx-4 h-[80vh] flex flex-col">
            <h3 class="text-xl font-bold text-gray-800 mb-4">Planes y Precios por Cantidad de Líneas</h3>
            <div id="pricingContent" class="flex-grow overflow-y-auto modal-content-scrollable pr-2">
                <!-- Pricing details will be loaded here by JavaScript -->
            </div>
            <div class="flex justify-end space-x-2 mt-4">
                <button id="closePricingModalBtn" class="bg-gray-400 hover:bg-gray-500 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out">Cerrar</button>
            </div>
        </div>
    </div>

    <!-- Firebase SDKs -->
    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInAnonymously, signInWithCustomToken, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, addDoc, onSnapshot, doc, updateDoc, deleteDoc, query } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // Global variables provided by the Canvas environment
        // NOTE: These variables are placeholders for a Google Cloud environment (like Canvas)
        // If you are running this locally without such an environment,
        // you will need to replace `__app_id` and `__firebase_config` with your actual Firebase project details.
        // For local testing, you can uncomment and fill in the following:
        // const appId = 'YOUR_FIREBASE_PROJECT_ID'; // e.g., 'my-awesome-project-12345'
        // const firebaseConfig = {
        //     apiKey: "YOUR_API_KEY",
        //     authDomain: "YOUR_AUTH_DOMAIN",
        //     projectId: "YOUR_PROJECT_ID",
        //     storageBucket: "YOUR_STORAGE_BUCKET",
        //     messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
        //     appId: "YOUR_APP_ID"
        // };
        // const initialAuthToken = ''; // Leave empty for anonymous sign-in or provide a token

        // For local testing without a Canvas environment, you can set dummy values
        // or comment out the __app_id and __firebase_config lines and use the commented block above
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        const firebaseConfig = JSON.parse(typeof __firebase_config !== 'undefined' ? __firebase_config : '{}');
        const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : '';
        
        let db;
        let auth;
        let currentUserId = '';
        let editingId = null; // Stores the ID of the portability being edited
        let currentPortabilitiesData = []; // Stores the latest fetched portability data
        let portingPhoneNumbers = []; // Array to store dynamically entered phone numbers

        // Updated Entel Plans - used for assignment in the form (aligned with image names)
        const mockPlans = [
            'Sin asignar',
            'Plan Móvil 350 GB',
            'Plan Móvil + LIBRE',
            'Plan Móvil LIBRE + ROAMING',
        ];

        // Detailed pricing data from the provided image (TOTAL values for modal)
        const pricingDetails = {
            "Plan Móvil 350 GB": {
                "1": 11043, "2": 20138, "3": 30207, "4": 40276, "5": 50345,
                "6": 60414, "7": 70483, "8": 80552, "9": 90621, "10": 100690,
                "11": 103609, "12": 113028, "13": 122447, "14": 131866, "15": 141285,
                "16": 150704, "17": 160123, "18": 169542, "19": 178961, "20": 188380,
                "21": 197799, "22": 207218, "23": 216637, "24": 226056, "25": 235475,
                "26": 244894, "27": 254313, "28": 263732, "29": 273151
            },
            "Plan Móvil + LIBRE": {
                "1": 13194, "2": 22188, "3": 33282, "4": 41972, "5": 52645,
                "6": 62958, "7": 73451, "8": 83944, "9": 94437, "10": 104930,
                "11": 108834, "12": 118722, "13": 128616, "14": 138510, "15": 148410,
                "16": 158304, "17": 168192, "18": 178092, "19": 187986, "20": 197880,
                "21": 207774, "22": 217662, "23": 227562, "24": 237456, "25": 247350,
                "26": 257244, "27": 267132, "28": 277032, "29": 286926
            },
            "Plan Móvil LIBRE + ROAMING": {
                "1": 14294, "2": 24740, "3": 37110, "4": 47276, "5": 59095,
                "6": 70914, "7": 82733, "8": 94552, "9": 106371, "10": 118190,
                "11": 123959, "12": 135228, "13": 146497, "14": 157766, "15": 169035,
                "16": 180304, "17": 191573, "18": 202842, "19": 214111, "20": 225380,
                "21": 236649, "22": 247918, "23": 259187, "24": 270456, "25": 281725,
                "26": 292994, "27": 304263, "28": 315532, "29": 326801
            }
        };

        // Per-line pricing data from the provided image (Valor Plan for message generation)
        const perLinePricingDetails = {
            "Plan Móvil 350 GB": {
                "1": 11043,
                "2-3": 10069,
                "4-10": 10069, // Note: This value is the same as 2-3 for 350GB plan as per image
                "11-29": 9419
            },
            "Plan Móvil + LIBRE": {
                "1": 13194,
                "2-3": 11094,
                "4-10": 10493,
                "11-29": 9894
            },
            "Plan Móvil LIBRE + ROAMING": {
                "1": 14294,
                "2-3": 12370,
                "4-10": 11819,
                "11-29": 11269
            }
        };

        // Plan features data
        const planFeatures = {
            "Plan Móvil 350 GB": [
                "•	📞 Minutos libres",
                "•	📱 Redes sociales gratis",
                "•	💬 1500 SMS",
                "•	🚀 5G para que disfrute de internet de alta velocidad",
                "•	📶 La mejor cobertura en todo el territorio Nacional"
            ],
            "Plan Móvil + LIBRE": [
                "•	📞 Minutos libres",
                "•	📱 Redes sociales ilimitadas",
                "•	💬 SMS ilimitados",
                "•	🚀 5G para que disfrute de internet de alta velocidad",
                "•	📶 La mejor cobertura en todo el territorio Nacional"
            ],
            "Plan Móvil LIBRE + ROAMING": [
                "•	📞 Minutos libres",
                "•	📱 Redes sociales ilimitadas",
                "•	💬 SMS ilimitados",
                "•	🌐 Roaming incluido para viajar sin preocupaciones",
                "•	🚀 5G para que disfrute de internet de alta velocidad",
                "•	📶 La mejor cobertura en todo el territorio Nacional"
            ],
            "Sin asignar": [] // No specific features if plan is not assigned
        };

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
        const sameAddressCheckbox = document.getElementById('sameAddressCheckbox'); // New checkbox
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

        // Pricing Modal Elements
        const pricingModal = document.getElementById('pricingModal');
        const pricingContent = document.getElementById('pricingContent');
        const closePricingModalBtn = document.getElementById('closePricingModalBtn');


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
                // Check if firebaseConfig is populated. If not, inform the user about local setup.
                if (Object.keys(firebaseConfig).length === 0 && appId === 'default-app-id') {
                    console.warn("Firebase configuration not found. Running in demo mode. Data will not be persisted.");
                    userIdDisplay.textContent = "DEMO (Sin Firebase)";
                    // Set up a mock data system for demo purposes
                    setupMockDataSystem();
                    return; // Exit as Firebase won't be initialized
                }

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

        // Mock Data System for local testing without Firebase config
        let mockPortabilities = [];
        let nextMockId = 1;

        function setupMockDataSystem() {
            console.log("Setting up mock data system.");
            // Load from localStorage if available
            try {
                const storedData = localStorage.getItem('mockPortabilities');
                if (storedData) {
                    mockPortabilities = JSON.parse(storedData);
                    nextMockId = mockPortabilities.reduce((maxId, item) => Math.max(maxId, parseInt(item.id.replace('mock_', ''))), 0) + 1;
                }
            } catch (e) {
                console.error("Error loading mock data from localStorage", e);
                mockPortabilities = [];
            }
            renderPortabilities(mockPortabilities); // Initial render
            // Override Firestore functions with mock versions
            window.addDoc = async (colRef, data) => {
                const newId = `mock_${nextMockId++}`;
                const newItem = { id: newId, ...data, planAsignado: mockPlans[0] };
                mockPortabilities.push(newItem);
                localStorage.setItem('mockPortabilities', JSON.stringify(mockPortabilities));
                renderPortabilities(mockPortabilities);
                return { id: newId };
            };
            window.updateDoc = async (docRef, data) => {
                const idToUpdate = docRef.id;
                const index = mockPortabilities.findIndex(p => p.id === idToUpdate);
                if (index !== -1) {
                    mockPortabilities[index] = { ...mockPortabilities[index], ...data };
                    localStorage.setItem('mockPortabilities', JSON.stringify(mockPortabilities));
                    renderPortabilities(mockPortabilities);
                }
            };
            window.deleteDoc = async (docRef) => {
                const idToDelete = docRef.id;
                mockPortabilities = mockPortabilities.filter(p => p.id !== idToDelete);
                localStorage.setItem('mockPortabilities', JSON.stringify(mockPortabilities));
                renderPortabilities(mockPortabilities);
            };
            // Simulate onSnapshot
            window.onSnapshot = (queryRef, callback) => {
                callback({
                    docs: mockPortabilities.map(p => ({ id: p.id, data: () => p }))
                });
                // In a real mock, you might need a way to trigger this callback on changes
                // For this simple demo, we just call it once on load.
            };
            window.doc = (db, collectionPath, id) => ({ id: id }); // Mock doc function
            window.collection = (db, path) => ({ path: path }); // Mock collection function
            window.query = (collectionRef) => collectionRef; // Mock query function
        }


        // Set up real-time listener for portabilities
        function setupRealtimeListener() {
            // Check if db is initialized (i.e., not in demo mode)
            if (!db) {
                console.warn("Firestore not initialized. Running in demo mode. Data is from mock system.");
                return;
            }
            if (!currentUserId) {
                console.warn("Current user ID not available for Firestore listener.");
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
                            <button data-id="${p.id}" class="send-whatsapp-btn bg-green-600 hover:bg-green-700 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out flex items-center justify-center transform hover:scale-105">
                                <svg class="w-5 h-5 mr-2" viewBox="0 0 24 24" fill="currentColor" xmlns="http://www.w3.org/2000/svg"><path d="M12.04 2C7.38 2 3.65 5.69 3.65 10.33C3.65 12.01 4.14 13.56 5 14.9L4.08 18L7.26 17.1C8.55 17.8 10.02 18.15 11.51 18.15H11.53C16.18 18.15 19.92 14.46 19.92 9.81C19.92 5.16 16.18 2 12.04 2ZM15.02 12.93C14.86 13.3 14.53 13.52 14.16 13.6C13.79 13.68 13.43 13.61 13.06 13.52C12.7 13.43 11.53 13.05 10.15 11.83C8.78 10.61 7.86 9.27 7.7 9C7.54 8.73 7.37 8.52 7.54 8.24C7.71 7.96 7.93 7.89 8.1 7.68C8.26 7.47 8.43 7.26 8.6 7.05C8.76 6.84 8.93 6.64 9.1 6.55C9.27 6.46 9.43 6.46 9.59 6.46C9.76 6.46 9.93 6.46 10.09 6.46C10.26 6.46 10.34 6.46 10.43 6.63C10.6 6.8 10.93 7.6 10.99 7.74C11.06 7.88 11.12 8.01 10.95 8.21C10.78 8.41 10.62 8.54 10.45 8.75C10.28 8.95 10.12 9.15 10.06 9.25C9.99 9.35 9.83 9.49 10.02 9.81C10.20 10.13 10.87 11.01 11.75 11.66C12.44 12.18 13.04 12.63 13.53 12.87C13.97 13.09 14.28 13.16 14.45 13.09C14.62 13.02 14.86 12.77 15.02 12.56C15.19 12.35 15.35 12.29 15.52 12.35C15.69 12.42 15.86 12.55 15.93 12.72C16 12.89 16 12.98 15.93 13.06C15.86 13.14 15.77 13.26 15.02 12.93Z"></path></svg>
                                Enviar por WhatsApp
                            </button>
                            <!-- NEW BUTTON: Planes y Precios -->
                            <button data-id="${p.id}" class="show-pricing-btn bg-gray-600 hover:bg-gray-700 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out flex items-center justify-center transform hover:scale-105">
                                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fillRule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-11a1 1 0 10-2 0v2H7a1 1 0 100 2h2v2a1 1 0 102 0v-2h2a1 1 0 100-2h-2V7z" clipRule="evenodd"></path></svg>
                                Planes y Precios
                            </button>
                            <button data-id="${p.id}" class="verify-giro-btn bg-indigo-500 hover:bg-indigo-600 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out flex items-center justify-center transform hover:scale-105">
                                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fillRule="evenodd" d="M10 2a1 1 0 00-1 1v1a1 1 0 001 1h4a1 1 0 001-1V3a1 1 0 00-1-1h-4zm0 6a1 1 0 00-1 1v7a1 1 0 001 1h4a1 1 0 001-1V9a1 1 0 00-1-1h-4z" clipRule="evenodd"></path></svg>
                                VERIFICAR GIRO COMERCIAL
                            </button>
                            <button data-id="${p.id}" class="check-debt-entel-btn bg-red-600 hover:bg-red-700 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out flex items-center justify-center transform hover:scale-105">
                                <svg class="w-5 h-5 mr-2" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fillRule="evenodd" d="M4 4a2 2 0 00-2 2v8a2 2 0 002 2h12a2 2 0 002-2V6a2 2 0 00-2-2H4zm0 2h12v8H4V6zm-2 3a2 2 0 012-2h12a2 2 0 012 2v4a2 2 0 01-2 2H4a2 2 0 01-2-2V9z" clipRule="evenodd"></path></svg>
                                DEUDA ENTEL NO CASTIGADA
                            </button>
                            <button data-id="${p.id}" class="check-debt-wom-btn bg-pink-600 hover:bg-pink-700 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out flex items-center justify-center transform hover:scale-105">
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
                            <button data-id="${p.id}" class="send-requirements-whatsapp-btn bg-blue-700 hover:bg-blue-800 text-white font-bold py-2 px-4 rounded-lg shadow-md transition duration-300 ease-in-out flex items-center justify-center transform hover:scale-105">
                                <svg class="w-5 h-5 mr-2" viewBox="0 0 24 24" fill="currentColor" xmlns="http://www.w3.org/2000/svg"><path d="M12.04 2C7.38 2 3.65 5.69 3.65 10.33C3.65 12.01 4.14 13.56 5 14.9L4.08 18L7.26 17.1C8.55 17.8 10.02 18.15 11.51 18.15H11.53C16.18 18.15 19.92 14.46 19.92 9.81C19.92 5.16 16.18 2 12.04 2ZM15.02 12.93C14.86 13.3 14.53 13.52 14.16 13.6C13.79 13.68 13.43 13.61 13.06 13.52C12.7 13.43 11.53 13.05 10.15 11.83C8.78 10.61 7.86 9.27 7.7 9C7.54 8.73 7.37 8.52 7.54 8.24C7.71 7.96 7.93 7.89 8.1 7.68C8.26 7.47 8.43 7.26 8.6 7.05C8.76 6.84 8.93 6.64 9.1 6.55C9.27 6.46 9.43 6.46 9.59 6.46C9.76 6.46 9.93 6.46 10.09 6.46C10.26 6.46 10.34 6.46 10.43 6.63C10.6 6.8 10.93 7.6 10.99 7.74C11.06 7.88 11.12 8.01 10.95 8.21C10.78 8.41 10.62 8.54 10.45 8.75C10.28 8.95 10.12 9.15 10.06 9.25C9.99 9.35 9.83 9.49 10.02 9.81C10.20 10.13 10.87 11.01 11.75 11.66C12.44 12.18 13.04 12.63 13.53 12.87C13.97 13.09 14.28 13.16 14.45 13.09C14.62 13.02 14.86 12.77 15.02 12.56C15.19 12.35 15.35 12.29 15.52 12.35C15.69 12.42 15.86 12.55 15.93 12.72C16 12.89 16 12.98 15.93 13.06C15.86 13.14 15.77 13.26 15.02 12.93Z"></path></svg>
                                SOLICITAR REQUISITOS (WhatsApp)
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

                document.querySelectorAll('.send-whatsapp-btn').forEach(button => {
                    button.addEventListener('click', (e) => {
                        const id = e.currentTarget.dataset.id;
                        const portability = currentPortabilitiesData.find(p => p.id === id);
                        if (portability) {
                            handleSendWhatsApp(portability);
                        }
                    });
                });
                
                // NEW: Event listener for the "Show Pricing" button
                document.querySelectorAll('.show-pricing-btn').forEach(button => {
                    button.addEventListener('click', () => {
                        showPricingModal();
                    });
                });

                // External Link Buttons
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

                document.querySelectorAll('.check-crm-btn').forEach(button => {
                    button.addEventListener('click', () => {
                        window.open('https://master.smartcrm.cl/gestion/home.html', '_blank');
                    });
                });

                // NEW: Event listener for the "Send Requirements by WhatsApp" button
                document.querySelectorAll('.send-requirements-whatsapp-btn').forEach(button => {
                    button.addEventListener('click', (e) => {
                        const id = e.currentTarget.dataset.id;
                        const portability = currentPortabilitiesData.find(p => p.id === id);
                        if (portability) {
                            handleSendRequirementsWhatsApp(portability);
                        }
                    });
                });
            }
        }

        // Function to render dynamic phone number input fields
        function renderPhoneNumberInputs(count, initialValues = []) {
            // Clear any existing errors before re-rendering inputs
            clearDynamicPhoneNumberErrors();

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
                if (initialValues[i]) {
                    input.value = initialValues[i];
                    portingPhoneNumbers[i] = initialValues[i]; // Initialize global array with existing values
                }
                input.addEventListener('input', (e) => {
                    portingPhoneNumbers[i] = e.target.value;
                    validateSinglePhoneNumber(e.target); // Validate format on input
                    validateDuplicatePhoneNumbers(); // Re-validate duplicates on input change
                });
            }
            // After rendering, re-validate all for initial display if needed
            portingPhoneNumbers.forEach((num, index) => {
                const input = document.getElementById(`portingNumber_${index}`);
                if (input) {
                    validateSinglePhoneNumber(input);
                }
            });
            validateDuplicatePhoneNumbers(); // Initial duplicate check when inputs are rendered/re-rendered
        }

        // Function to clear all dynamic phone number error messages
        function clearDynamicPhoneNumberErrors() {
            const numInputs = parseInt(numLineasInput.value);
            for (let i = 0; i < numInputs; i++) {
                const errorDisplay = document.getElementById(`portingNumberError_${i}`);
                const input = document.getElementById(`portingNumber_${i}`);
                if (errorDisplay) {
                    errorDisplay.classList.add('hidden');
                    errorDisplay.textContent = '';
                }
                if (input) {
                    input.classList.remove('border-red-500');
                    input.classList.add('border-gray-300');
                }
            }
        }


        // Function to validate a single phone number input format
        function validateSinglePhoneNumber(inputElement) {
            const errorDisplay = document.getElementById(`portingNumberError_${inputElement.id.split('_')[1]}`);
            const value = inputElement.value.trim();
            
            // Allow empty if it's an optional secondary line
            if (value.length === 0) {
                errorDisplay.classList.add('hidden');
                inputElement.classList.remove('border-red-500');
                inputElement.classList.add('focus:border-blue-500');
                return true;
            }

            // Validate if not empty
            if (!/^\d{9}$/.test(value)) { // Ensures exactly 9 digits
                errorDisplay.textContent = 'El número debe tener exactamente 9 dígitos numéricos.';
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

        // Function to validate duplicate phone numbers
        function validateDuplicatePhoneNumbers() {
            let isValid = true;
            clearDynamicPhoneNumberErrors(); // Clear all errors first

            const seenNumbers = new Set();
            const duplicateNumbers = new Set();

            for (let i = 0; i < portingPhoneNumbers.length; i++) {
                const currentNum = portingPhoneNumbers[i].trim();
                const inputElement = document.getElementById(`portingNumber_${i}`);
                const errorDisplay = document.getElementById(`portingNumberError_${i}`);

                if (currentNum) { // Only check non-empty numbers for duplicates
                    if (seenNumbers.has(currentNum)) {
                        duplicateNumbers.add(currentNum);
                        isValid = false;
                    } else {
                        seenNumbers.add(currentNum);
                    }
                }
            }

            // Now, iterate again to mark all instances of duplicates
            if (!isValid) {
                for (let i = 0; i < portingPhoneNumbers.length; i++) {
                    const currentNum = portingPhoneNumbers[i].trim();
                    const inputElement = document.getElementById(`portingNumber_${i}`);
                    const errorDisplay = document.getElementById(`portingNumberError_${i}`);

                    if (duplicateNumbers.has(currentNum)) {
                        inputElement.classList.add('border-red-500');
                        inputElement.classList.remove('focus:border-blue-500');
                        if (errorDisplay) {
                            errorDisplay.textContent = 'Número repetido. Por favor, modifique.';
                            errorDisplay.classList.remove('hidden');
                        }
                    }
                }
            }
            return isValid;
        }

        // Validate RUT format
        function validateRut(rut) {
            // This is a basic regex for RUT format. A full RUT validation (including digit verifier)
            // would require a more complex algorithm (Modulo 11).
            // This regex accepts: 12.345.678-9 or 12345678-9
            if (!/^(\d{1,2}\.\d{3}\.\d{3}-[\dkK]|\d{7,8}-[\dkK])$/.test(rut)) {
                return false;
            }
            // For a more robust validation, you'd integrate a Modulo 11 check here.
            return true;
        }

        // Basic form validation
        function validateForm() {
            let isValid = true;

            // Clear previous general errors
            document.querySelectorAll('.text-red-500').forEach(el => {
                if (!el.id.startsWith('portingNumberError_')) { // Don't clear dynamic number errors here
                    el.classList.add('hidden');
                }
            });
            document.querySelectorAll('.border-red-500').forEach(el => {
                if (!el.id.startsWith('portingNumber_')) { // Don't clear dynamic number borders here
                    el.classList.remove('border-red-500');
                    el.classList.add('border-gray-300');
                }
            });

            // Validate RUT
            if (!rutInput.value.trim() || !validateRut(rutInput.value.trim())) {
                rutInput.classList.add('border-red-500');
                showMessage('Por favor, ingresa un RUT válido (ej: 12.345.678-9 o 12345678-9).');
                isValid = false;
            }

            // Validate Nombre
            if (!nombreInput.value.trim()) {
                nombreInput.classList.add('border-red-500');
                showMessage('El nombre del cliente es obligatorio.');
                isValid = false;
            }

            // Validate Operador Origen
            if (!operadorOrigenInput.value) {
                operadorOrigenInput.classList.add('border-red-500');
                showMessage('Debes seleccionar un operador de origen.');
                isValid = false;
            }

            // Validate Fecha Portabilidad
            if (!fechaPortabilidadInput.value) {
                fechaPortabilidadInput.classList.add('border-red-500');
                showMessage('La fecha de portabilidad es obligatoria.');
                isValid = false;
            }

            // Validate numLineas
            const numLinesVal = parseInt(numLineasInput.value);
            if (isNaN(numLinesVal) || numLinesVal < 1 || numLinesVal > 29) {
                numLineasError.textContent = 'Debe ingresar entre 1 y 29 líneas.';
                numLineasError.classList.remove('hidden');
                numLineasInput.classList.add('border-red-500');
                isValid = false;
            } else {
                numLineasError.classList.add('hidden');
                numLineasInput.classList.remove('border-red-500');
            }

            // Validate primary phone number input if numLineas is 1 AND the input is visible
            if (numLinesVal === 1 && !numeroInput.parentElement.classList.contains('hidden')) {
                if (!numeroInput.value.trim() || !/^\d{9}$/.test(numeroInput.value.trim())) {
                    numeroInput.classList.add('border-red-500');
                    showMessage('Para una sola línea, el "Número de Teléfono (Principal)" es obligatorio y debe tener 9 dígitos.');
                    isValid = false;
                }
            } else if (numLinesVal > 1) { // If multiple lines are selected, validate dynamic inputs
                for (let i = 0; i < numLinesVal; i++) {
                    const input = document.getElementById(`portingNumber_${i}`);
                    if (!input || !validateSinglePhoneNumber(input)) { // Check individual format
                        isValid = false;
                    }
                    if (!input.value.trim()) { // All dynamically added numbers must be filled
                        input.classList.add('border-red-500');
                        const errorDisplay = document.getElementById(`portingNumberError_${i}`);
                        if (errorDisplay) {
                            errorDisplay.textContent = 'Este número es obligatorio.';
                            errorDisplay.classList.remove('hidden');
                        }
                        isValid = false;
                    }
                }
                // Also run duplicate validation if multiple lines
                if (!validateDuplicatePhoneNumbers()) {
                    isValid = false;
                    // No need to show general message here, specific errors will highlight fields
                }
            }


            // Validate Correo Electrónico
            if (!correoElectronicoInput.value.trim()) {
                correoElectronicoInput.classList.add('border-red-500');
                showMessage('El correo electrónico es obligatorio.');
                isValid = false;
            } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(correoElectronicoInput.value.trim())) {
                correoElectronicoInput.classList.add('border-red-500');
                showMessage('Por favor, ingresa un correo electrónico válido.');
                isValid = false;
            }

            return isValid;
        }


        // Handle adding or updating a portability
        async function handleAddOrUpdatePortability() {
            if (!validateForm()) {
                return; // Stop if form is not valid
            }

            const data = {
                // Only save primary number if it's a single line entry (numLineas == 1)
                numero: parseInt(numLineasInput.value) === 1 ? numeroInput.value.trim() : '', 
                rut: rutInput.value.trim(),
                nombre: nombreInput.value.trim(),
                operadorOrigen: operadorOrigenInput.value,
                fechaPortabilidad: fechaPortabilidadInput.value,
                numLineas: parseInt(numLineasInput.value),
                lineasPortar: portingPhoneNumbers.filter(num => num.trim() !== ''), // Store only filled numbers
                direccionCliente: direccionClienteInput.value.trim(),
                direccionEntrega: direccionEntregaInput.value.trim(),
                correoElectronico: correoElectronicoInput.value.trim(),
                planAsignado: mockPlans[0], // Default to "Sin asignar"
                userId: currentUserId, // Store the user who added/edited this
                timestamp: new Date().toISOString(), // Add timestamp for sorting/tracking
            };

            try {
                if (editingId) {
                    // Update existing document
                    if (db) { // Check if Firebase is initialized
                        const docRef = doc(db, `artifacts/${appId}/public/data/entelPortabilities`, editingId);
                        await updateDoc(docRef, data);
                    } else { // Mock update
                        await window.updateDoc(window.doc(null, null, editingId), data); // Using mock updateDoc
                    }
                    showMessage('Portabilidad actualizada con éxito!');
                    editingId = null; // Reset editing state
                    addUpdateBtn.textContent = 'Agregar Portabilidad';
                    cancelEditBtn.classList.add('hidden');
                    formTitle.textContent = 'Registrar Nueva Portabilidad';
                } else {
                    // Add new document
                    if (db) { // Check if Firebase is initialized
                        const colRef = collection(db, `artifacts/${appId}/public/data/entelPortabilities`);
                        await addDoc(colRef, data);
                    } else { // Mock add
                        await window.addDoc(null, data); // Using mock addDoc
                    }
                    showMessage('Portabilidad agregada con éxito!');
                }
                clearForm();
            } catch (error) {
                console.error("Error saving portability:", error);
                showMessage(`Error al guardar portabilidad: ${error.message}`);
            }
        }

        // Handle editing a portability
        function handleEditPortability(portability) {
            editingId = portability.id;
            formTitle.textContent = 'Editar Portabilidad Existente';
            
            // Populate form fields with existing data
            numeroInput.value = portability.numero || ''; 
            rutInput.value = portability.rut || '';
            nombreInput.value = portability.nombre || '';
            operadorOrigenInput.value = portability.operadorOrigen || '';
            fechaPortabilidadInput.value = portability.fechaPortabilidad || '';
            numLineasInput.value = portability.numLineas || 1; // Default to 1 if not set

            // Set visibility of primary number input based on numLineas
            if (parseInt(numLineasInput.value) === 1) {
                numeroInput.parentElement.classList.remove('hidden');
            } else {
                numeroInput.parentElement.classList.add('hidden');
            }

            // Populate dynamic phone numbers
            renderPhoneNumberInputs(portability.numLineas || 1, portability.lineasPortar || []);
            
            direccionClienteInput.value = portability.direccionCliente || '';
            direccionEntregaInput.value = portability.direccionEntrega || '';
            correoElectronicoInput.value = portability.correoElectronico || '';

            // Set the state of the sameAddressCheckbox if direccionEntrega is populated
            if (direccionEntregaInput.value === direccionClienteInput.value && direccionClienteInput.value !== '') {
                sameAddressCheckbox.checked = true;
            } else {
                sameAddressCheckbox.checked = false;
            }

            addUpdateBtn.textContent = 'Actualizar Portabilidad';
            cancelEditBtn.classList.remove('hidden');

            // Scroll to the top of the form
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        // Handle deleting a portability
        async function handleDeletePortability(id) {
            if (confirm('¿Estás seguro de que quieres eliminar esta portabilidad?')) {
                try {
                    if (db) {
                        const docRef = doc(db, `artifacts/${appId}/public/data/entelPortabilities`, id);
                        await deleteDoc(docRef);
                    } else { // Mock delete
                        await window.deleteDoc(window.doc(null, null, id)); // Using mock deleteDoc
                    }
                    showMessage('Portabilidad eliminada con éxito.');
                    if (editingId === id) { // If deleting the one being edited
                        clearForm();
                        editingId = null;
                        addUpdateBtn.textContent = 'Agregar Portabilidad';
                        cancelEditBtn.classList.add('hidden');
                        formTitle.textContent = 'Registrar Nueva Portabilidad';
                    }
                } catch (error) {
                    console.error("Error deleting portability:", error);
                    showMessage(`Error al eliminar portabilidad: ${error.message}`);
                }
            }
        }

        // Handle assigning the next plan
        async function handleAssignPlan(id, currentPlan) {
            const currentIndex = mockPlans.indexOf(currentPlan);
            const nextIndex = (currentIndex + 1) % mockPlans.length; // Cycle through plans
            const nextPlan = mockPlans[nextIndex];

            try {
                if (db) {
                    const docRef = doc(db, `artifacts/${appId}/public/data/entelPortabilities`, id);
                    await updateDoc(docRef, { planAsignado: nextPlan });
                } else { // Mock update for demo mode
                    const index = mockPortabilities.findIndex(p => p.id === id);
                    if (index !== -1) {
                        mockPortabilities[index].planAsignado = nextPlan;
                        localStorage.setItem('mockPortabilities', JSON.stringify(mockPortabilities));
                        renderPortabilities(mockPortabilities); // Re-render to show change
                    }
                }
                showMessage(`Plan actualizado a: ${nextPlan}`);
            } catch (error) {
                console.error("Error updating plan:", error);
                showMessage(`Error al actualizar plan: ${error.message}`);
            }
        }

        // Helper function to get formatted pricing text for a given plan and number of lines
        function getFormattedPricingForPlan(planName, numLines) {
            const planPricing = perLinePricingDetails[planName];
            if (!planPricing) {
                return "Precio no disponible para este plan o cantidad de líneas.";
            }

            let pricingText = "";
            let pricePerLine = 0; // This will store the price per line for the given range

            if (numLines === 1) {
                pricePerLine = planPricing["1"];
                pricingText = `$${pricePerLine.toLocaleString('es-CL')} IVA INCLUIDO`;
            } else if (numLines >= 2 && numLines <= 3) {
                pricePerLine = planPricing["2-3"];
                pricingText = `$${pricePerLine.toLocaleString('es-CL')} CADA UNA (con descuento multilínea) si porta de 2 a 3 líneas.`;
            } else if (numLines >= 4 && numLines <= 10) {
                pricePerLine = planPricing["4-10"];
                pricingText = `¡Así es, de 4 a 10 líneas (actualmente ${numLines} líneas) le quedan a solo $${pricePerLine.toLocaleString('es-CL')} cada una!`;
            } else if (numLines >= 11 && numLines <= 29) {
                pricePerLine = planPricing["11-29"];
                pricingText = `Si son 11 o más (actualmente ${numLines} líneas), le sale a $${pricePerLine.toLocaleString('es-CL')}`;
            } else {
                pricingText = "Precios especiales aplican, consúltenos para más detalles sobre la cantidad de líneas.";
            }
            return pricingText;
        }


        // Handle generating message
        function handleGenerateMessage(portability) {
            const fullName = portability.nombre.trim();
            const firstName = fullName.split(' ')[0];
            let salutationPrefix;

            // Simple heuristic for salutation: 'Estimada, Srta.' for feminine, 'Estimado, Sr.' for masculine, otherwise general
            if (firstName.toLowerCase().endsWith('a') || fullName.toLowerCase().includes("sra.")) { // Added check for "Sra."
                salutationPrefix = "Estimada, Srta.";
            } else if (firstName.toLowerCase().endsWith('o') || fullName.toLowerCase().includes("sr.")) { // Added check for "Sr."
                salutationPrefix = "Estimado, Sr.";
            } else {
                salutationPrefix = "Estimado/a cliente,"; // More general formal
            }
            
            let message = `${salutationPrefix} ${fullName},\n\n`; // Always use full name as per example

            message += `Junto con saludar, le escribo en seguimiento a la llamada que recibió de nuestro ejecutivo hoy.\n\n`;
            message += `Mi nombre es Erik Sosa y soy parte del equipo de Entel. El motivo de mi contacto es formalizar la excelente oferta que le mencionaron para que pueda disfrutar de los beneficios de nuestro ${portability.planAsignado}.\n\n`;

            // Dynamic total pricing based on numLineas
            const planName = portability.planAsignado;
            const numLines = portability.numLineas;
            let pricingSentence = "";

            if (planName !== 'Sin asignar' && numLines >= 1) {
                const totalPrice = pricingDetails[planName]?.[numLines.toString()];
                if (totalPrice !== undefined) {
                    pricingSentence += `El valor TOTAL de su plan para ${numLines} línea(s) es de *$${totalPrice.toLocaleString('es-CL')} IVA INCLUIDO*.\n`; // Highlight total price

                    const perLinePricing = perLinePricingDetails[planName];
                    if (perLinePricing) {
                        if (numLines === 1) {
                            pricingSentence += `Este es el valor para 1 línea individual.\n`;
                        } else if (numLines >= 2 && numLines <= 3) {
                            const priceForRange = perLinePricing["2-3"];
                            pricingSentence += `Con el descuento multilínea, cada línea le queda a $${priceForRange.toLocaleString('es-CL')}. Este precio aplica si porta de 2 a 3 líneas.\n`;
                        } else if (numLines >= 4 && numLines <= 10) {
                            const priceForRange = perLinePricing["4-10"];
                            pricingSentence += `Para ${numLines} líneas, cada una le queda a solo $${priceForRange.toLocaleString('es-CL')}.\n`;
                        } else if (numLines >= 11 && numLines <= 29) {
                            const priceForRange = perLinePricing["11-29"];
                            pricingSentence += `Si son ${numLines} líneas o más, cada una le sale a $${priceForRange.toLocaleString('es-CL')}.\n`;
                        }
                    }
                    pricingSentence += `\n`; // Add extra line break after pricing details
                } else {
                    pricingSentence += `No fue posible determinar el precio total para el plan ${planName} con ${numLines} línea(s). Por favor, verifique la configuración de planes y líneas.\n\n`;
                }
            } else if (planName === 'Sin asignar') {
                pricingSentence += `Para este servicio, el plan aún no ha sido asignado. Por favor, asigne un plan para obtener la información de precios.\n\n`;
            }
            message += pricingSentence;


            message += `Este plan le ofrece:\n`;
            const features = planFeatures[portability.planAsignado] || [];
            features.forEach(feature => {
                message += `${feature}\n`;
            });
            message += `\n`;


            message += `Esperamos que esta propuesta sea de su agrado y le invitamos a unirse a la familia Entel. Quedamos a su disposición para cualquier consulta adicional.\n\n`;

            message += `¡OFERTA EXCLUSIVA POR PORTABILIDAD CON NOSOTROS! �\n`;
            message += `Le recordamos que se lleva el mejor servicio y además le REGALAMOS UNA CUENTA STREAMING GRATIS por 30 DÍAS por CADA LÍNEA. Podrá elegir entre Disney+, Netflix, Prime Video, YouTube Premium, ¡y mucho más! Estas cuentas son TOTALMENTE RENOVABLES. 🎁🍿 Le invitamos a compartirlas con su familia o amigos.\n\n`;


            message += `Para que avancemos CON LA PORTABILIDAD A ENTEL CHILE, ¡es súper fácil! Solo necesitamos:\n`;
            message += `•	📄 La ÚLTIMA BOLETA de su compañía anterior (por ambos lados)\n`;
            message += `•	🆔 Su RUT por (ambos lados) del titular: ${portability.rut}\n\n`; // Automatically insert RUT


            message += `¡Quedo atento a cualquier consulta! 🤓 ¡No pierda esta oportunidad de oro!\n\n`;
            message += `Saludos,\nErik Sosa\nSupervisor Comercial Entel Empresas`;

            generatedMessageTextarea.value = message;
            messageModal.classList.remove('hidden');
        }

        // Function to generate and open WhatsApp message
        function handleSendWhatsApp(portability) {
            // Basic validation for phone number
            const phoneNumber = portability.numero || (portability.lineasPortar && portability.lineasPortar.length > 0 ? portability.lineasPortar[0] : null);

            if (!phoneNumber) {
                showMessage('No hay número de teléfono principal o de línea a portar para enviar el mensaje de WhatsApp.', 5000);
                return;
            }

            // Re-use the message generation logic from handleGenerateMessage for WhatsApp
            const fullName = portability.nombre.trim();
            const firstName = fullName.split(' ')[0];
            let salutationPrefix;

            if (firstName.toLowerCase().endsWith('a') || fullName.toLowerCase().includes("sra.")) {
                salutationPrefix = "Estimada, Srta.";
            } else if (firstName.toLowerCase().endsWith('o') || fullName.toLowerCase().includes("sr.")) {
                salutationPrefix = "Estimado, Sr.";
            } else {
                salutationPrefix = "Estimado/a cliente,";
            }

            let message = `${salutationPrefix} ${fullName},\n\n`;

            message += `Junto con saludar, le escribo en seguimiento a la llamada que recibió de nuestro ejecutivo hoy.\n\n`;
            message += `Mi nombre es Erik Sosa y soy parte del equipo de Entel. El motivo de mi contacto es formalizar la excelente oferta que le mencionaron para que pueda disfrutar de los beneficios de nuestro ${portability.planAsignado}.\n\n`;
            
            // Dynamic total pricing based on numLineas for WhatsApp
            const planName = portability.planAsignado;
            const numLines = portability.numLineas;
            let pricingSentence = "";

            if (planName !== 'Sin asignar' && numLines >= 1) {
                const totalPrice = pricingDetails[planName]?.[numLines.toString()];
                if (totalPrice !== undefined) {
                    pricingSentence += `El valor TOTAL de su plan para ${numLines} línea(s) es de *$${totalPrice.toLocaleString('es-CL')} IVA INCLUIDO*.\n`;

                    const perLinePricing = perLinePricingDetails[planName];
                    if (perLinePricing) {
                        if (numLines === 1) {
                            pricingSentence += `Este es el valor para 1 línea individual.\n`;
                        } else if (numLines >= 2 && numLines <= 3) {
                            const priceForRange = perLinePricing["2-3"];
                            pricingSentence += `Con el descuento multilínea, cada línea le queda a $${priceForRange.toLocaleString('es-CL')}. Este precio aplica si porta de 2 a 3 líneas.\n`;
                        } else if (numLines >= 4 && numLines <= 10) {
                            const priceForRange = perLinePricing["4-10"];
                            pricingSentence += `Para ${numLines} líneas, cada una le queda a solo $${priceForRange.toLocaleString('es-CL')}.\n`;
                        } else if (numLines >= 11 && numLines <= 29) {
                            const priceForRange = perLinePricing["11-29"];
                            pricingSentence += `Si son ${numLines} líneas o más, cada una le sale a $${priceForRange.toLocaleString('es-CL')}.\n`;
                        }
                    }
                    pricingSentence += `\n`;
                } else {
                    pricingSentence += `No fue posible determinar el precio total para el plan ${planName} con ${numLines} línea(s). Por favor, verifique la configuración de planes y líneas.\n\n`;
                }
            } else if (planName === 'Sin asignar') {
                pricingSentence += `Para este servicio, el plan aún no ha sido asignado. Por favor, asigne un plan para obtener la información de precios.\n\n`;
            }
            message += pricingSentence;

            message += `Este plan le ofrece:\n`;
            const features = planFeatures[portability.planAsignado] || [];
            features.forEach(feature => {
                message += `${feature}\n`;
            });
            message += `\n`;

            message += `Esperamos que esta propuesta sea de su agrado y le invitamos a unirse a la familia Entel. Quedamos a su disposición para cualquier consulta adicional.\n\n`;

            message += `¡OFERTA EXCLUSIVA POR PORTABILIDAD CON NOSOTROS! 🤩\n`;
            message += `Le recordamos que se lleva el mejor servicio y además le REGALAMOS UNA CUENTA STREAMING GRATIS por 30 DÍAS por CADA LÍNEA. Podrá elegir entre Disney+, Netflix, Prime Video, YouTube Premium, ¡y mucho más! Estas cuentas son TOTALMENTE RENOVABLES. 🎁🍿 Le invitamos a compartirlas con su familia o amigos.\n\n`;
            
            message += `Para que avancemos CON LA PORTABILIDAD A ENTEL CHILE, ¡es súper fácil! Solo necesitamos:\n`;
            message += `•	📄 La ÚLTIMA BOLETA de su compañía anterior (por ambos lados)\n`;
            message += `•	🆔 Su RUT por (ambos lados) del titular: ${portability.rut}\n\n`;

            message += `¡Quedo atento a cualquier consulta! 🤓 ¡No pierda esta oportunidad de oro!\n\n`;
            message += `Saludos,\nErik Sosa\nSupervisor Comercial Entel Empresas`;


            const encodedMessage = encodeURIComponent(message);
            // Assuming Chile's country code is 56. Ensure the phone number doesn't already have +56.
            const whatsappUrl = `https://wa.me/56${phoneNumber.replace(/\s+/g, '')}?text=${encodedMessage}`; 

            window.open(whatsappUrl, '_blank');
        }

        // NEW: Function to send requirements message via WhatsApp
        function handleSendRequirementsWhatsApp(portability) {
            const fullName = portability.nombre.trim();
            const firstName = fullName.split(' ')[0];
            let salutationPrefix;

            if (firstName.toLowerCase().endsWith('a') || fullName.toLowerCase().includes("sra.")) {
                salutationPrefix = "Hola, Srta.";
            } else if (firstName.toLowerCase().endsWith('o') || fullName.toLowerCase().includes("sr.")) {
                salutationPrefix = "Hola, Sr.";
            } else {
                salutationPrefix = "Hola";
            }

            // Hardcoded WhatsApp number for requirements
            const targetPhoneNumber = "58416146924"; // The requested number +58416146924 without the '+' and stripped of initial 0 if present.

            let message = `${salutationPrefix} ${fullName},\n\n`;
            message += `Para avanzar con su portabilidad a Entel Chile, por favor envíenos las siguientes fotos *adjuntándolas en este chat de WhatsApp*:\n\n`; // Clarify attachment
            message += `•	📄 La ÚLTIMA BOLETA de su compañía anterior (por ambos lados)\n`;
            message += `•	🆔 Su RUT por (ambos lados) del titular: ${portability.rut}\n\n`;
            message += `¡Quedo atento a su envío! ¡Muchas gracias! 😊`;

            const encodedMessage = encodeURIComponent(message);
            const whatsappUrl = `https://wa.me/${targetPhoneNumber.replace(/\s+/g, '')}?text=${encodedMessage}`;
            window.open(whatsappUrl, '_blank');
        }


        // Function to display the pricing modal
        function showPricingModal() {
            let contentHtml = '';
            for (const planName in pricingDetails) {
                // Skip "Sin asignar" as it has no pricing details
                if (planName === "Sin asignar") {
                    continue;
                }

                contentHtml += `<div class="mb-6 p-4 border border-blue-200 rounded-lg bg-blue-50">`;
                contentHtml += `<h4 class="text-xl font-semibold text-blue-700 mb-3">${planName}</h4>`;
                contentHtml += `<table class="min-w-full bg-white border border-gray-200 rounded-lg overflow-hidden">`;
                contentHtml += `<thead>`;
                contentHtml += `<tr class="bg-blue-100 text-gray-700 uppercase text-sm leading-normal">`;
                contentHtml += `<th class="py-3 px-6 text-left">N° Líneas</th>`;
                contentHtml += `<th class="py-3 px-6 text-right">TOTAL</th>`;
                contentHtml += `</tr>`;
                contentHtml += `</thead>`;
                contentHtml += `<tbody class="text-gray-600 text-sm font-light">`;

                const planPrices = pricingDetails[planName];
                // Sort keys numerically to ensure 1, 2, 3... order
                const sortedKeys = Object.keys(planPrices).sort((a, b) => parseInt(a) - parseInt(b));

                sortedKeys.forEach(numLines => {
                    const price = planPrices[numLines];
                    if (price !== undefined) {
                        contentHtml += `<tr class="border-b border-gray-200 hover:bg-gray-100">`;
                        contentHtml += `<td class="py-3 px-6 text-left whitespace-nowrap font-medium">${numLines}</td>`;
                        contentHtml += `<td class="py-3 px-6 text-right whitespace-nowrap">$${price.toLocaleString('es-CL')}</td>`;
                        contentHtml += `</tr>`;
                    }
                });
                contentHtml += `</tbody>`;
                contentHtml += `</table>`;
                contentHtml += `</div>`;
            }
            pricingContent.innerHTML = contentHtml;
            pricingModal.classList.remove('hidden');
        }


        // Clear the form fields
        function clearForm() {
            numeroInput.value = '';
            rutInput.value = '';
            nombreInput.value = '';
            operadorOrigenInput.value = '';
            fechaPortabilidadInput.value = '';
            numLineasInput.value = '1'; // Reset to 1 line
            phoneNumbersContainer.innerHTML = ''; // Clear dynamic inputs
            portingPhoneNumbers = []; // Clear the array
            direccionClienteInput.value = '';
            direccionEntregaInput.value = '';
            correoElectronicoInput.value = '';
            sameAddressCheckbox.checked = false; // Uncheck the checkbox
            editingId = null;
            addUpdateBtn.textContent = 'Agregar Portabilidad';
            cancelEditBtn.classList.add('hidden');
            formTitle.textContent = 'Registrar Nueva Portabilidad';
            numeroInput.parentElement.classList.remove('hidden'); // Ensure primary number is visible

            // Clear any validation errors
            document.querySelectorAll('.border-red-500').forEach(el => {
                el.classList.remove('border-red-500');
                el.classList.add('border-gray-300');
            });
            document.querySelectorAll('.text-red-500').forEach(el => el.classList.add('hidden'));
            renderPhoneNumberInputs(1); // Render one empty input by default after clear
        }

        // Event Listeners
        addUpdateBtn.addEventListener('click', handleAddOrUpdatePortability);
        cancelEditBtn.addEventListener('click', clearForm);
        closeModalBtn.addEventListener('click', () => messageModal.classList.add('hidden'));
        closePricingModalBtn.addEventListener('click', () => pricingModal.classList.add('hidden')); // Close pricing modal

        copyMessageBtn.addEventListener('click', async () => {
            try {
                // For clipboard copy, use execCommand as navigator.clipboard.writeText might be restricted in iframes
                generatedMessageTextarea.select();
                document.execCommand('copy');
                showMessage('Mensaje copiado al portapapeles!', 2000);
            } catch (err) {
                console.error('Error al copiar el mensaje: ', err);
                showMessage('Error al copiar el mensaje. Por favor, cópialo manualmente.', 3000);
            }
        });

        // Event listener for numLineas change to dynamically render phone number inputs
        numLineasInput.addEventListener('input', (e) => {
            const count = parseInt(e.target.value);
            if (!isNaN(count) && count >= 1 && count <= 29) {
                renderPhoneNumberInputs(count);
                numLineasError.classList.add('hidden'); // Hide error if valid
            } else {
                numLineasError.textContent = 'Debe ingresar entre 1 y 29 líneas.';
                numLineasError.classList.remove('hidden'); // Show error if invalid
                phoneNumbersContainer.innerHTML = ''; // Clear dynamic inputs
                portingPhoneNumbers = [];
            }

            // If numLineas is 1, ensure the primary number input is visible
            if (count === 1) {
                numeroInput.parentElement.classList.remove('hidden');
            } else {
                numeroInput.parentElement.classList.add('hidden');
                numeroInput.value = ''; // Clear primary number if multiple lines
            }
        });

        // New event listener for the "same address" checkbox
        sameAddressCheckbox.addEventListener('change', () => {
            if (sameAddressCheckbox.checked) {
                direccionEntregaInput.value = direccionClienteInput.value;
            } else {
                direccionEntregaInput.value = ''; // Clear the field if unchecked
            }
        });


        // Initial setup
        document.addEventListener('DOMContentLoaded', () => {
            document.getElementById('currentYear').textContent = new Date().getFullYear();
            renderPhoneNumberInputs(parseInt(numLineasInput.value)); // Render initial phone number inputs based on default value
            initializeFirebase(); // Initialize Firebase when DOM is ready
            // Check initial state for numLineas to hide/show primary number input
            if (parseInt(numLineasInput.value) > 1) {
                numeroInput.parentElement.classList.add('hidden');
            }
        });
    </script>
</body>
</html>
