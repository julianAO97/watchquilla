<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Catálogo de Relojes - Precios para Distribuidores y Clientes</title>
    <style>
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --accent-color: #e74c3c;
            --light-color: #ecf0f1;
            --dark-color: #34495e;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f7fa;
            color: #333;
            line-height: 1.6;
        }
        
        header {
            background: linear-gradient(135deg, var(--primary-color), var(--dark-color));
            color: white;
            padding: 1.5rem;
            text-align: center;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        
        .user-type-selector {
            display: flex;
            justify-content: center;
            margin: 1.5rem 0;
            gap: 1rem;
        }
        
        .user-btn {
            padding: 0.8rem 1.5rem;
            border: none;
            border-radius: 30px;
            background-color: var(--light-color);
            color: var(--dark-color);
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .user-btn.active {
            background-color: var(--secondary-color);
            color: white;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 1rem;
        }
        
        .filters {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            margin-bottom: 2rem;
            justify-content: center;
        }
        
        .filter-btn {
            padding: 0.5rem 1rem;
            border: 1px solid var(--secondary-color);
            border-radius: 20px;
            background-color: transparent;
            color: var(--secondary-color);
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .filter-btn:hover, .filter-btn.active {
            background-color: var(--secondary-color);
            color: white;
        }
        
        .watch-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
            gap: 2rem;
            margin-bottom: 3rem;
        }
        
        .watch-card {
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        
        .watch-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
        }
        
        .watch-image {
            height: 200px;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: #f8f9fa;
        }
        
        .watch-image img {
            max-width: 100%;
            max-height: 100%;
            object-fit: cover;
        }
        
        .watch-info {
            padding: 1.5rem;
        }
        
        .watch-brand {
            font-size: 0.9rem;
            color: var(--secondary-color);
            font-weight: 600;
            text-transform: uppercase;
            margin-bottom: 0.5rem;
        }
        
        .watch-name {
            font-size: 1.2rem;
            font-weight: 700;
            margin-bottom: 1rem;
            color: var(--primary-color);
        }
        
        .watch-features {
            margin-bottom: 1rem;
            font-size: 0.9rem;
            color: #666;
        }
        
        .price-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-top: 1.5rem;
            padding-top: 1rem;
            border-top: 1px solid #eee;
        }
        
        .final-price {
            font-size: 1.3rem;
            font-weight: 700;
            color: var(--accent-color);
        }
        
        .distributor-price {
            font-size: 1rem;
            color: #666;
            text-decoration: line-through;
            display: none;
        }
        
        .distributor-mode .distributor-price {
            display: block;
        }
        
        .distributor-mode .final-price {
            color: var(--secondary-color);
            font-size: 1.1rem;
        }
        
        .price-label {
            font-size: 0.8rem;
            color: #888;
            display: block;
            margin-bottom: 0.3rem;
        }
        
        footer {
            background-color: var(--dark-color);
            color: white;
            text-align: center;
            padding: 2rem;
            margin-top: 2rem;
        }
        
        @media (max-width: 768px) {
            .watch-grid {
                grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
            }
            
            .user-type-selector {
                flex-direction: column;
                align-items: center;
            }
            
            .user-btn {
                width: 80%;
            }
        }
    </style>
</head>
<body>
    <header>
        <h1>Catálogo de Relojes Exclusivos</h1>
        <p>Seleccione su tipo de usuario para ver los precios correspondientes</p>
        
        <div class="user-type-selector">
            <button class="user-btn active" id="final-client-btn">Cliente Final</button>
            <button class="user-btn" id="distributor-btn">Distribuidor/Vendedor</button>
        </div>
    </header>
    
    <div class="container">
        <div class="filters">
            <button class="filter-btn active">Todos</button>
            <button class="filter-btn">Deportivos</button>
            <button class="filter-btn">Elegantes</button>
            <button class="filter-btn">Inteligentes</button>
            <button class="filter-btn">Clásicos</button>
        </div>
        
        <div class="watch-grid" id="watch-catalog">
            <!-- Los relojes se cargarán dinámicamente con JavaScript -->
        </div>
    </div>
    
    <footer>
        <p>Catálogo de Relojes &copy; 2023 - Precios sujetos a cambio sin previo aviso</p>
    </footer>

    <script>
        // Datos de ejemplo para el catálogo
        const watches = [
            {
                id: 1,
                brand: "Rolex",
                name: "Submariner Date",
                features: ["Automático", "300m resistente al agua", "Cronómetro"],
                image: "https://via.placeholder.com/300x200/3498db/ffffff?text=Rolex+Submariner",
                finalPrice: 9500,
                distributorPrice: 7125
            },
            {
                id: 2,
                brand: "Omega",
                name: "Seamaster Professional",
                features: ["Cronómetro", "300m resistente al agua", "Cerámica"],
                image: "https://via.placeholder.com/300x200/e74c3c/ffffff?text=Omega+Seamaster",
                finalPrice: 5200,
                distributorPrice: 3900
            },
            {
                id: 3,
                brand: "Tag Heuer",
                name: "Carrera Calibre 5",
                features: ["Automático", "41mm", "Cuero genuino"],
                image: "https://via.placeholder.com/300x200/2c3e50/ffffff?text=Tag+Heuer+Carrera",
                finalPrice: 3200,
                distributorPrice: 2400
            },
            {
                id: 4,
                brand: "Casio",
                name: "G-Shock GA-2100",
                features: ["Resistente a impactos", "200m resistente al agua", "Calendario"],
                image: "https://via.placeholder.com/300x200/34495e/ffffff?text=Casio+G-Shock",
                finalPrice: 120,
                distributorPrice: 84
            },
            {
                id: 5,
                brand: "Apple",
                name: "Watch Series 8",
                features: ["GPS", "Monitor cardiaco", "Resistente al agua"],
                image: "https://via.placeholder.com/300x200/7f8c8d/ffffff?text=Apple+Watch",
                finalPrice: 429,
                distributorPrice: 343
            },
            {
                id: 6,
                brand: "Tissot",
                name: "Le Locle Powermatic 80",
                features: ["Automático", "80h reserva de marcha", "Caja de acero"],
                image: "https://via.placeholder.com/300x200/16a085/ffffff?text=Tissot+Le+Locle",
                finalPrice: 675,
                distributorPrice: 506
            }
        ];

        // Referencias a elementos del DOM
        const watchCatalog = document.getElementById('watch-catalog');
        const finalClientBtn = document.getElementById('final-client-btn');
        const distributorBtn = document.getElementById('distributor-btn');
        const filterBtns = document.querySelectorAll('.filter-btn');
        
        // Estado de la aplicación
        let isDistributorMode = false;
        
        // Función para formatear precios
        function formatPrice(price) {
            return new Intl.NumberFormat('es-ES', {
                style: 'currency',
                currency: 'EUR'
            }).format(price);
        }
        
        // Función para renderizar los relojes en el catálogo
        function renderWatches() {
            watchCatalog.innerHTML = '';
            
            watches.forEach(watch => {
                const watchCard = document.createElement('div');
                watchCard.className = 'watch-card';
                
                watchCard.innerHTML = `
                    <div class="watch-image">
                        <img src="${watch.image}" alt="${watch.brand} ${watch.name}">
                    </div>
                    <div class="watch-info">
                        <div class="watch-brand">${watch.brand}</div>
                        <h3 class="watch-name">${watch.name}</h3>
                        <ul class="watch-features">
                            ${watch.features.map(feature => `<li>${feature}</li>`).join('')}
                        </ul>
                        <div class="price-container">
                            <div>
                                <span class="price-label">${isDistributorMode ? 'Precio distribuidor' : 'Precio final'}</span>
                                <div class="final-price">${formatPrice(isDistributorMode ? watch.distributorPrice : watch.finalPrice)}</div>
                            </div>
                            ${isDistributorMode ? `
                                <div>
                                    <span class="price-label">Precio al público</span>
                                    <div class="distributor-price">${formatPrice(watch.finalPrice)}</div>
                                </div>
                            ` : ''}
                        </div>
                    </div>
                `;
                
                watchCatalog.appendChild(watchCard);
            });
            
            // Aplicar clase al body para el modo distribuidor
            if (isDistributorMode) {
                document.body.classList.add('distributor-mode');
            } else {
                document.body.classList.remove('distributor-mode');
            }
        }
        
        // Event listeners para los botones de tipo de usuario
        finalClientBtn.addEventListener('click', () => {
            isDistributorMode = false;
            finalClientBtn.classList.add('active');
            distributorBtn.classList.remove('active');
            renderWatches();
        });
        
        distributorBtn.addEventListener('click', () => {
            isDistributorMode = true;
            distributorBtn.classList.add('active');
            finalClientBtn.classList.remove('active');
            renderWatches();
        });
        
        // Event listeners para los filtros
        filterBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                filterBtns.forEach(b => b.classList.remove('active'));
                btn.classList.add('active');
                // Aquí iría la lógica de filtrado real
            });
        });
        
        // Inicializar el catálogo
        renderWatches();
    </script>
</body>
</html>
