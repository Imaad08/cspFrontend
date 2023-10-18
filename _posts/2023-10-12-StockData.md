<head>
    <style>
        body {
            background-color: white;
            color: white;
            font-family: Arial, sans-serif;
            padding: 20px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            border: 1px solid white;
        }
        select, button {
            font-size: 16px;
            padding: 10px;
            margin-bottom: 20px;
            border: 1px solid white;
            color: white;
        }
        select {
            width: 100%;
        }
        button {
            cursor: pointer;
        }
        button:hover, select:hover {
            color: gray;
        }
        #graph {
            width: 100%;
        }
    </style>
    <script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
</head>
<body>
    <label for="stock-select">Select a stock:</label>
    <select id="stock-select">
        <option value="AAPL">AAPL</option>
        <option value="GOOGL">GOOGL</option>
        <option value="AMZN">AMZN</option>
        <option value="META">META</option>
        <option value="TSLA">TSLA</option>
        <option value="SBUX">SBUX</option>
        <option value="ETSY">ETSY</option>
        <option value="EBAY">EBAY</option>
    </select>
    <button onclick="getStockGraph()">Display Graph</button>
    <div id="graph"></div>
    <script>
        function getStockGraph() {
            const selectedStock = document.getElementById('stock-select').value;
            const apiUrl = 'http://127.0.0.1:8282/api/stocks/stock_graph/' + selectedStock;
            fetch(apiUrl)
                .then(response => response.json())
                .then(graphData => {
                    Plotly.newPlot('graph', graphData.data, graphData.layout);
                })
                .catch(error => console.error('Error:', error));
        }
    </script>
</body>
