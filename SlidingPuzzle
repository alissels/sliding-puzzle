import React from "react";
import "./styles.css";

const startGame = () => {
  const values = [0, 1, 2, 3, 4, 5, 6, 7, 8];

  const firstRow = [],
    secondRow = [],
    thirdRow = [];
  while (values.length) {
    const random = Math.floor(Math.random() * values.length);
    console.log(random);
    if (firstRow.length < 3) {
      firstRow.push(values.splice(random, 1)[0]);
    } else if (secondRow.length < 3) {
      secondRow.push(values.splice(random, 1)[0]);
    } else {
      thirdRow.push(values.splice(random, 1)[0]);
    }
  }

  return [firstRow, secondRow, thirdRow];
};

const getGame = () => {
  let game = startGame();
  return game;
};

export default function SlidingPuzzle() {
  const [game, setGame] = React.useState([]);
  const [moves, setMoves] = React.useState(0);

  React.useEffect(() => {
    setGame(getGame());
  }, []);

  const moveItem = (x, y) => {
    if (checkNeighbours(x, y) || checkNeighbours(x, y, 2)) {
      const openSpace = checkNeighbours(x, y) || checkNeighbours(x, y, 2);

      const newGame = game.map((row) => row.slice());

      if (x === openSpace.x && y < openSpace.y) {
        newGame[openSpace.x][openSpace.y] = game[x][y + 1];
        newGame[x][y + 1] = newGame[x][y];
        newGame[x][y] = 0;
      } else if (x === openSpace.x && y > openSpace.y) {
        newGame[openSpace.x][openSpace.y] = game[x][y - 1];
        newGame[x][y - 1] = newGame[x][y];
        newGame[x][y] = 0;
      }

      if (y === openSpace.y && x < openSpace.x) {
        newGame[openSpace.x][openSpace.y] = game[x + 1][y];
        newGame[x + 1][y] = newGame[x][y];
        newGame[x][y] = 0;
      } else if (y === openSpace.y && x > openSpace.x) {
        newGame[openSpace.x][openSpace.y] = game[x - 1][y];
        newGame[x - 1][y] = newGame[x][y];
        newGame[x][y] = 0;
      }

      setGame(newGame);
      setMoves(moves + 1);
    }
  };

  const checkNeighbours = (x, y, d = 1) => {
    const neighbours = [];

    if (game[x][y] !== 0) {
      neighbours.push(
        game[x - d] && game[x - d][y] === 0 && { x: x - d, y: y }
      );
      neighbours.push(game[x][y + d] === 0 && { x: x, y: y + d });
      neighbours.push(
        game[x + d] && game[x + d][y] === 0 && { x: x + d, y: y }
      );
      neighbours.push(game[x][y - d] === 0 && { x: x, y: y - d });
    }

    const openSpace = neighbours.find((el) => typeof el === "object");

    return openSpace;
  };

  const resetGame = () => {
    setGame(getGame());
    setMoves(0);
  };

  return (
    <div className="SlidingPuzzle">
      {<h3 style={{ color: "#F84AA7" }}>Number of Moves: {moves}</h3>}
      <div
        style={{
          display: "inline-block",
          padding: 5
        }}
      >
        {game.map((row, i) => (
          <div
            key={i}
            style={{
              display: "flex"
            }}
          >
            {row.map((col, j) => {
              return (
                <div
                  key={`${i}-${j}`}
                  onClick={() => moveItem(i, j)}
                  style={{
                    display: "flex",
                    justifyContent: "center",
                    alignItems: "center",
                    width: 100,
                    height: 100,
                    margin: 2,
                    backgroundColor: "#FF3562",
                    borderRadius: 5,
                    cursor: "pointer",
                    userSelect: "none"
                  }}
                >
                  <span style={{ fontSize: "2rem", fontWeight: "bold" }}>
                    {col !== 0 && col}
                  </span>
                </div>
              );
            })}
          </div>
        ))}
      </div>
      <p>
        <button
          onClick={() => {
            resetGame();
          }}
        >
          Reset Game
        </button>
      </p>
    </div>
  );
}
