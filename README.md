<!--
Programa: Movimento do quadrado
Nome: Andressa Pezzolato de Almeida - Nº:2 - Turma: 2B
Nome: Eduardo Rodrigues - Nº:6.
Nome: Enzo Feitosa - Nº:7.
Nome: Gabrielle Léo - Nº:10.
Nome: Guilherme Holanda- Nº:12.
DESCRIÇÃO:Esse código cria um pequeno jogo onde uma peça(quadrado) pode ser movida em quatro 
direções dentro de um canvas. .
-->
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <title>Componentes</title>
    <meta charset="UTF-8">
    <style>
        canvas {
            border: 1px solid #d3d3d3;
            background-color: #000000;
        }
    </style>
    <script>
        var cor = 'purple';
        var cont = 1;
        var myGamePiece;
        var moveStep = 10; // Número de pixels que o quadrado se moverá em cada clique
        var moveInterval;

        function startGame() {
            myGamePiece = new component(30, 30, "ciano", 10, 120);
            myGameArea.start();
        }

        var myGameArea = {
            canvas: document.createElement("canvas"),
            start: function() {
                this.canvas.width = 400;
                this.canvas.height = 270;
                this.context = this.canvas.getContext("2d");
                document.body.insertBefore(this.canvas, document.body.childNodes[0]);
                this.interval = setInterval(updateGameArea, 20);
            },
            clear: function() {
                this.context.clearRect(0, 0, this.canvas.width, this.canvas.height);
            }
        }

        function component(width, height, color, x, y) {
            this.width = width;
            this.height = height;
            this.x = x;
            this.y = y;
            this.update = function() {
                var ctx = myGameArea.context;
                if (cont % 10 == 0)
                    cor = 'purple';
                else
                    cor = 'pink';
                ctx.fillStyle = cor;
                ctx.fillRect(this.x, this.y, this.width, this.height);
                cont++;
            }
        }

        function updateGameArea() {
            myGameArea.clear();
            myGamePiece.update();
        }

        function move(direction) {
            if (direction === 'up' && myGamePiece.y > 0) myGamePiece.y -= moveStep;
            else if (direction === 'down' && myGamePiece.y < myGameArea.canvas.height - myGamePiece.height) myGamePiece.y += moveStep;
            else if (direction === 'left' && myGamePiece.x > 0) myGamePiece.x -= moveStep;
            else if (direction === 'right' && myGamePiece.x < myGameArea.canvas.width - myGamePiece.width) myGamePiece.x += moveStep;
        }

        function startMovement(direction) {
            moveInterval = setInterval(() => move(direction), 100);
        }

        function stopMovement() {
            clearInterval(moveInterval);
        }
    </script>
</head>
<body onload="startGame();">
    <div>
        <button onmousedown="startMovement('up')" onmouseup="stopMovement()" onmouseleave="stopMovement()">Cima</button>
        <button onmousedown="startMovement('down')" onmouseup="stopMovement()" onmouseleave="stopMovement()">Baixo</button>
        <button onmousedown="startMovement('left')" onmouseup="stopMovement()" onmouseleave="stopMovement()">Esquerda</button>
        <button onmousedown="startMovement('right')" onmouseup="stopMovement()" onmouseleave="stopMovement()">Direita</button>
    </div>
</body>
</html>
