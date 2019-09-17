import { print, image, random, promptString } from "introcs";
import { Sprite, Container, Application, Rectangle, Graphics, DisplayObject, Text } from "pixi.js";



/*HOW TO PLAY: 
Move left character with WASD, right character with arrowkeys,
Space Bar will randomly place ball to start the round,
Players have to get the ball and take it to the opposite baseline without being touched earing you a point,
Players colliding will restart the round,
Game is played to 5 points,
*/

let speed: number = 2;

let richard = 0;
let seth = 0;

// let text = new PIXI.Text("This is a PixiJS text", {fontFamily : "Arial", fontSize: 24, fill : 0xff1010, align : "center"});

let resetPlayer1 = (): void => {
    player1.x = 900;
    player1.y = 270;
    player1.scale.x = 0.15;
    player1.scale.y = 0.15;       
};


let resetPlayer2 = (): void => {
    player2.x = 0;
    player2.y = 270;
    player2.scale.x = 0.15;
    player2.scale.y = 0.15;
};

let resetbasketball = (): void => {
    basketball.x = 472.5;
    basketball.y = 292.5;  
};

const app: Application = new Application(945, 585);
document.body.appendChild(app.view);

class Blob {
    sprite: Sprite;
    direction: number = 1;
    constructor(sprite: Sprite) {
        this.sprite = sprite;
    }
}

let background: Sprite = Sprite.fromImage("./bballcourt.png");
background.scale.x = .48;
background.scale.y = .48;
background.x = 0;
background.y = 0;

app.stage.addChild(background);

let player1: Sprite = Sprite.fromImage("./rich.png");
app.stage.addChild(player1);
player1.scale.x = 0.15;
player1.scale.y = 0.15;
player1.x = 900;
player1.y = 270;


let player2: Sprite = Sprite.fromImage("./mrraether.png");
app.stage.addChild(player2);
player2.scale.x = 0.15;
player2.scale.y = 0.15;
player2.x = 0;
player2.y = 270;

let finishLine: Sprite = Sprite.fromImage("./finish.png");
app.stage.addChild(finishLine);
finishLine.scale.y = 1.5;
finishLine.x = -130;

let finishLine1: Sprite = Sprite.fromImage("./finish.png");
app.stage.addChild(finishLine1);
finishLine1.scale.y = 1.5;
finishLine1.x = 944;

let basketball: Sprite = Sprite.fromImage("./bball.png");
app.stage.addChild(basketball);
basketball.scale.x = 0.025;
basketball.scale.y = 0.025;
basketball.x = 472.5;
basketball.y = 292.5;

window.onkeydown = (e: KeyboardEvent): void => {
    console.log("calling p1 listener");
    const LEFT: number = 37;
    const LEFT1: number = 65;
    const UP: number = 38;
    const UP1: number = 87;
    const RIGHT: number = 39;
    const RIGHT1: number = 68;
    const DOWN: number = 40;
    const DOWN1: number = 83;
    const STEP: number = 5;
    if (e.keyCode === LEFT) {
        player1.x -= STEP;
    } else if (e.keyCode === UP) {
        player1.y -= STEP;
    } else if (e.keyCode === RIGHT) {
        player1.x += STEP;
    } else if (e.keyCode === DOWN) {
        player1.y += STEP;
    } else if (e.keyCode === LEFT1) {
        player2.x -= STEP;       
    } else if (e.keyCode === UP1) {
        player2.y -= STEP;
    } else if (e.keyCode === RIGHT1) {
        player2.x += STEP;
    } else if (e.keyCode === DOWN1) {
        player2.y += STEP;
    }
};

let L: number = 0;
let R: number = 0;
let D: number = 0;
let U: number = 0;
let L1: number = 0;
let R1: number = 0;
let D1: number = 0;
let U1: number = 0;

window.addEventListener("keyup", (e: KeyboardEvent): void  => {
    console.log("key: " + e.keyCode);
    const LEFT: number = 37;
    const UP: number = 38;
    const RIGHT: number = 39;
    const DOWN: number = 40;
    const LEFT1: number = 65;
    const UP1: number = 87;
    const RIGHT1: number = 68;
    const DOWN1: number = 83;

    if (e.keyCode === LEFT) {
        L = 0;
    } else if (e.keyCode === UP) {
        U = 0;
    } else if (e.keyCode === RIGHT) {
        R = 0;
    } else if (e.keyCode === DOWN) {
        D = 0;
    } else if (e.keyCode === LEFT1) {
        L1 = 0;
    } else if (e.keyCode === UP1) {
        U1 = 0;
    } else if (e.keyCode === RIGHT1) {
        R1 = 0;
    } else if (e.keyCode === DOWN1) {
        D1 = 0;
    }
});

window.addEventListener("keydown", (e: KeyboardEvent): void  => {
    console.log("key: " + e.keyCode);
    const LEFT: number = 37;
    const UP: number = 38;
    const RIGHT: number = 39;
    const DOWN: number = 40;
    const LEFT1: number = 65;
    const UP1: number = 87;
    const RIGHT1: number = 68;
    const DOWN1: number = 83;
    if (e.keyCode === LEFT) {
        L = -1;
    } else if (e.keyCode === UP) {
        U = -1;
    } else if (e.keyCode === RIGHT) {
        R = 1;
    } else if (e.keyCode === DOWN) {
        D = 1;
    } else if (e.keyCode === LEFT1) {
        L1 = -1;
    } else if (e.keyCode === UP1) {
        U1 = -1;
    } else if (e.keyCode === RIGHT1) {
        R1 = 1;
    } else if (e.keyCode === DOWN1) {
        D1 = 1;
    }
});

window.addEventListener("keydown", (e: KeyboardEvent): void  => {
    console.log("key: " + e.keyCode);
    const R: number = 32;
    if (e.keyCode === R) {
        basketball.x = random(50, 800);
        basketball.y = random(20, 400);
    }
  
});

let isColliding = (a: DisplayObject, b: DisplayObject): boolean => {
    const ab: Rectangle = a.getBounds();
    const bb: Rectangle = b.getBounds();
    return ab.x + ab.width > bb.x && ab.x < bb.x + bb.width && ab.y + ab.height > bb.y && ab.y < bb.y + bb.height;
};

let hasCollided = false;

app.ticker.add((delta: number): void => {

    player1.x += (L + R) * speed;
    player1.y += (U + D) * speed;
    player2.x += (L1 + R1) * speed;
    player2.y += (U1 + D1) * speed;

  

    if (isColliding(player1, basketball) && !hasCollided) {
        let currX = player1.x;
        let currY = player1.y;
        let currS = player1.scale;
        app.stage.removeChild(player1);
        app.stage.removeChild(basketball);
        player1 = Sprite.fromImage("./richwball.png");
        player1.x = currX;
        player1.y = currY;
        player1.scale = currS;
        app.stage.addChild(player1);
        hasCollided = true;
    }

    if (isColliding(player2, basketball) && !hasCollided) {
        let currX = player2.x;
        let currY = player2.y;
        let currS = player2.scale;
        app.stage.removeChild(player2);
        app.stage.removeChild(basketball);
        player2 = Sprite.fromImage("./sethwball.png");
        player2.x = currX;
        player2.y = currY;
        player2.scale = currS;
        app.stage.addChild(player2);
        hasCollided = true;
    }


    if (isColliding(player1, player2)) {
        app.stage.removeChild(player1);
        app.stage.removeChild(player2);
        player1 = Sprite.fromImage("./rich.png");
        player2 = Sprite.fromImage("./mrraether.png");
        app.stage.addChild(player1);
        app.stage.addChild(player2);
        app.stage.addChild(basketball);
        resetPlayer1();
        resetPlayer2();
        resetbasketball();
        hasCollided = false;
      
    }

    if (isColliding(player1, finishLine)) {
        richard++;
        if (richard >= 5) {
            window.location.assign("https://youtu.be/2FsnVCLYcrM?t=19");
        } else {
        app.stage.removeChild(player1);
        app.stage.removeChild(player2);
        player1 = Sprite.fromImage("./rich.png");
        player2 = Sprite.fromImage("./mrraether.png");
        app.stage.addChild(player1);
        app.stage.addChild(player2);
        app.stage.addChild(basketball);
        resetPlayer1();
        resetPlayer2();
        resetbasketball();
        hasCollided = false;
        }
    }
    if (isColliding(player2, finishLine1)) {
        seth++;
        if (seth >= 5) {
            window.location.assign("https://youtu.be/2FsnVCLYcrM?t=19");
        } else {
        app.stage.removeChild(player1);
        app.stage.removeChild(player2);
        player1 = Sprite.fromImage("./rich.png");
        player2 = Sprite.fromImage("./mrraether.png");
        app.stage.addChild(player1);
        app.stage.addChild(player2);
        app.stage.addChild(basketball);
        resetPlayer1();
        resetPlayer2();
        resetbasketball();
        hasCollided = false;
        }
    }


});

 
 // main();
