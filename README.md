<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>بروجكت </title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #F7F7F7;
            font-family: Arial, sans-serif;
        }
        .search-container {
            text-align: center;
        }
        input[type="text"] {
            padding: 10px;
            width: 250px;
            font-size: 16px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }
        .result {
            margin-top: 20px;
            font-size: 18px;
            color: #333;
        }
    </style>
</head>
<body>

    <!-- حاوية البحث -->
    <div class="search-container">
        <h2>بحث عن منتج</h2>
        <!-- حقل البحث وزر البحث -->
        <div style="margin-top: 20px;">
            <input type="text" id="productInput" placeholder="ادخل اسم المنتج أو  Code">
            <button onclick="searchProduct()">بحث</button>
        </div>
        <div class="result" id="result"></div>
    </div>

    <script>
        // تعريف قاعدة بيانات المنتجات
        const productDatabase ={
            1: { id: 1, name: "Laptop", price: 1500.00, category: "Electronics" },
            2: { id: 2, name: "Book", price: 15.00, category: "Books"},
            3: { id: 3, name: "Strawberry", price: 20.00, category: "fruit"}, 
            4: { id: 4, name: "ايس كريم", price: 100, category: "candy"},
            5: { id: 5, name: "بطاطس", price: 10.00, category:"خضراوات"}};

        // دالة لتوليد QR Code (محاكاة)
        function generateQRCode(productId) {
            return `QR_${productId}`;
        }

        // دالة للبحث عن منتج
        function searchProduct() {
            const input = document.getElementById("productInput").value.trim();
            const resultDiv = document.getElementById("result");

            // التحقق إذا كان المدخل فارغ
            if (!input) {
                resultDiv.innerText = "الرجاء إدخال اسم المنتج أو QR Code";
                return;
            }

            // التحقق إذا كان المدخل QR Code
            if (input.startsWith("QR_")) {
                const productId = parseInt(input.substring(3));
                if (productDatabase[productId]) {
                    displayProductInfo(productDatabase[productId]);
                } else {
                    resultDiv.innerText = "عذراً، المنتج المطلوب غير موجود";
                }
            } else {
                // البحث بالاسم أو رقم المنتج
                let foundProduct = null;
                for (const id in productDatabase) {
                    const product = productDatabase[id];
                    if (product.name.toLowerCase() === input.toLowerCase() || product.id === parseInt(input)) {
                        foundProduct = product;
                        break;
                    }
                }
                if (foundProduct) {
                    displayProductInfo(foundProduct);
                } else {
                    resultDiv.innerText = "عذراً، المنتج المطلوب غير موجود";
                }
            }
        }

        // دالة لعرض معلومات المنتج
        function displayProductInfo(product) {
            const resultDiv = document.getElementById("result");
            resultDiv.innerHTML = `
                <strong>رقم المنتج:</strong> ${product.id}<br>
                <strong>الاسم:</strong> ${product.name}<br>
                <strong>السعر:</strong> $${product.price}<br>
                <strong>الفئة:</strong> ${product.category}
            `;
        }
    </script>

</body>
</html>
