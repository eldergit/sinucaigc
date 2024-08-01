<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Football League Table</title>
    <style>
        table {
            width: 50%;
            border-collapse: collapse;
            margin: 20px auto;
        }
        th, td {
            border: 1px solid black;
            padding: 10px;
            text-align: center;
        }
        th {
            background-color: #f2f2f2;
        }
        form {
            width: 50%;
            margin: 20px auto;
            display: flex;
            justify-content: space-between;
        }
        input[type="text"] {
            width: 150px;
        }
        .form-group {
            display: flex;
            align-items: center;
        }
        .form-group label {
            margin-right: 10px;
        }
    </style>
    <font size="+2"><center><b>Rankeada Oficial da Sinuca do IGC</b></center></font>
    <script>
        const teams = {};

        function updateTable() {
            const winner = document.getElementById('winner').value.trim();
            const loser = document.getElementById('loser').value.trim();

            if (winner && loser && winner !== loser) {
                if (!teams[winner]) {
                    teams[winner] = { won: 0, lost: 0, points: 0 };
                }
                if (!teams[loser]) {
                    teams[loser] = { won: 0, lost: 0, points: 0 };
                }

                teams[winner].won += 1;
                teams[winner].points += 3;
                teams[loser].lost += 1;

                const sortedTeams = Object.keys(teams).map(name => ({
                    name,
                    ...teams[name]
                })).sort((a, b) => b.points - a.points);

                const tbody = document.querySelector('tbody');
                tbody.innerHTML = '';
                sortedTeams.forEach((team, index) => {
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td>${index + 1}</td>
                        <td>${team.name}</td>
                        <td>${team.won}</td>
                        <td>${team.lost}</td>
                        <td>${team.points}</td>
                    `;
                    tbody.appendChild(row);
                });

                document.getElementById('winner').value = '';
                document.getElementById('loser').value = '';
            } else {
                alert('Please enter valid names for both winner and loser.');
            }
        }
    </script>
</head>
<body>
    <form onsubmit="updateTable(); return false;">
        <div class="form-group">
            <label for="winner">Vencedor:</label>
            <input type="text" id="winner" name="winner">
        </div>
        <div class="form-group">
            <label for="loser">Perdedor:</label>
            <input type="text" id="loser" name="loser">
        </div>
        <button type="submit">Atualizar Tabela</button>
    </form>
    <table>
        <thead>
            <tr>
                <th>#</th>
                <th>Nome do Jogador</th>
                <th>Ganhou</th>
                <th>Perdeu</th>
                <th>Pontuação</th>
            </tr>
        </thead>
        <tbody>
            <!-- Rows will be dynamically added here -->
        </tbody>
    </table>
</body>
</html>
