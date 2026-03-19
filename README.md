<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Virement bancaire</title>

<style>
    body {
        margin: 0;
        font-family: Arial, sans-serif;
        background-color: #f2f2f2;
        display: flex;
        justify-content: center;
    }

    .container {
        width: 100%;
        max-width: 400px;
        background: white;
        min-height: 100vh;
        padding: 20px;
        box-sizing: border-box;
    }

    .header {
        text-align: center;
        font-weight: bold;
        font-size: 20px;
        margin-bottom: 30px;
    }

    .form-group {
        margin-bottom: 18px;
    }

    label {
        display: block;
        font-size: 14px;
        margin-bottom: 5px;
        color: #333;
    }

    input {
        width: 100%;
        padding: 12px;
        border-radius: 8px;
        border: 1px solid #ccc;
        font-size: 16px;
        box-sizing: border-box;
    }

    input:focus {
        outline: none;
        border-color: #e30613;
    }

    .error {
        color: red;
        font-size: 12px;
        display: none;
    }

    .btn {
        width: 100%;
        padding: 15px;
        background-color: #e30613;
        color: white;
        border: none;
        border-radius: 8px;
        font-size: 16px;
        font-weight: bold;
        cursor: pointer;
        margin-top: 20px;
    }

    .btn:active {
        opacity: 0.8;
    }

    .info {
        font-size: 12px;
        color: #666;
        margin-top: 10px;
        text-align: center;
    }

    .success {
        color: green;
        text-align: center;
        margin-top: 15px;
        display: none;
    }
</style>
</head>

<body>

<div class="container">
    <div class="header">Virement bancaire</div>

    <form id="form">
        <div class="form-group">
            <label>Nom du bénéficiaire</label>
            <input type="text" id="nom" placeholder="Ex : Jean Dupont">
            <div class="error" id="errorNom">Veuillez entrer un nom</div>
        </div>

        <div class="form-group">
            <label>IBAN du bénéficiaire</label>
            <input type="text" id="iban" placeholder="FR76 XXXX XXXX XXXX XXXX XXXX XXX">
            <div class="error" id="errorIban">IBAN invalide</div>
        </div>

        <div class="form-group">
            <label>Montant (€)</label>
            <input type="number" id="montant" placeholder="0,00">
            <div class="error" id="errorMontant">Montant invalide</div>
        </div>

        <button type="submit" class="btn">CONFIRMER LE VIREMENT</button>
    </form>

    <div class="success" id="successMsg">
        ✅ Virement confirmé avec succès !
    </div>

    <div class="info">
        Vérifiez les informations avant de confirmer.
    </div>
</div>

<script>
    const form = document.getElementById("form");

    function validateIBAN(iban) {
        iban = iban.replace(/\s+/g, '').toUpperCase();
        return /^[A-Z]{2}[0-9]{2}[A-Z0-9]{11,30}$/.test(iban);
    }

    form.addEventListener("submit", function(e) {
        e.preventDefault();

        let valid = true;

        const nom = document.getElementById("nom").value.trim();
        const iban = document.getElementById("iban").value.trim();
        const montant = document.getElementById("montant").value;

        // Reset erreurs
        document.querySelectorAll(".error").forEach(e => e.style.display = "none");

        if (nom === "") {
            document.getElementById("errorNom").style.display = "block";
            valid = false;
        }

        if (!validateIBAN(iban)) {
            document.getElementById("errorIban").style.display = "block";
            valid = false;
        }

        if (montant <= 0 || montant === "") {
            document.getElementById("errorMontant").style.display = "block";
            valid = false;
        }

        if (valid) {
            document.getElementById("successMsg").style.display = "block";
            form.reset();
        }
    });
</script>

</body>
</html>