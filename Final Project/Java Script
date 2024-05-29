const { useState } = React;

const CARD_TYPES = {
  EMPEROR: '皇帝',
  SLAVE: '奴隸',
  COMMONER: '平民'
};

const CARD_IMAGES = {
  [CARD_TYPES.EMPEROR]: 'https://i.postimg.cc/3xhff1dQ/32779.jpg',
  [CARD_TYPES.SLAVE]: 'https://i.postimg.cc/W1frqbRY/32781.jpg',
  [CARD_TYPES.COMMONER]: 'https://i.postimg.cc/zXrkqB5n/32780.jpg'
};

const EMPEROR_DECK = [
  { type: CARD_TYPES.EMPEROR, img: CARD_IMAGES[CARD_TYPES.EMPEROR] },
  { type: CARD_TYPES.COMMONER, img: CARD_IMAGES[CARD_TYPES.COMMONER] },
  { type: CARD_TYPES.COMMONER, img: CARD_IMAGES[CARD_TYPES.COMMONER] },
  { type: CARD_TYPES.COMMONER, img: CARD_IMAGES[CARD_TYPES.COMMONER] },
  { type: CARD_TYPES.COMMONER, img: CARD_IMAGES[CARD_TYPES.COMMONER] }
];
const SLAVE_DECK = [
  { type: CARD_TYPES.SLAVE, img: CARD_IMAGES[CARD_TYPES.SLAVE] },
  { type: CARD_TYPES.COMMONER, img: CARD_IMAGES[CARD_TYPES.COMMONER] },
  { type: CARD_TYPES.COMMONER, img: CARD_IMAGES[CARD_TYPES.COMMONER] },
  { type: CARD_TYPES.COMMONER, img: CARD_IMAGES[CARD_TYPES.COMMONER] },
  { type: CARD_TYPES.COMMONER, img: CARD_IMAGES[CARD_TYPES.COMMONER] }
];

function shuffleDeck(deck) {
  return deck.sort(() => Math.random() - 0.5);
}

function App() {
  const [playerHand, setPlayerHand] = useState([]);
  const [opponentHand, setOpponentHand] = useState([]);
  const [result, setResult] = useState(null);
  const [gameStarted, setGameStarted] = useState(false);
  const [playerRole, setPlayerRole] = useState('');
  const [playerChoice, setPlayerChoice] = useState('');
  const [opponentChoice, setOpponentChoice] = useState('');
  const [gameOver, setGameOver] = useState(false);
  const [isTie, setIsTie] = useState(false);

  const startGame = (role) => {
    setPlayerRole(role);
    if (role === CARD_TYPES.EMPEROR) {
      setPlayerHand(shuffleDeck([...EMPEROR_DECK]));
      setOpponentHand(shuffleDeck([...SLAVE_DECK]));
    } else {
      setPlayerHand(shuffleDeck([...SLAVE_DECK]));
      setOpponentHand(shuffleDeck([...EMPEROR_DECK]));
    }
    setResult(null);
    setGameStarted(true);
    setPlayerChoice('');
    setOpponentChoice('');
    setGameOver(false);
    setIsTie(false);
  };

  const resetGame = () => {
    setGameStarted(false);
    setPlayerRole('');
    setPlayerHand([]);
    setOpponentHand([]);
    setResult(null);
    setPlayerChoice('');
    setOpponentChoice('');
    setGameOver(false);
    setIsTie(false);
  };

  const continueGame = () => {
    setPlayerChoice('');
    setOpponentChoice('');
    setResult(null);
    setGameOver(false);
    setIsTie(false);
  };

  const chooseCard = (choice, index) => {
    setPlayerChoice(choice);
    const opponentCardIndex = Math.floor(Math.random() * opponentHand.length);
    const opponentCard = opponentHand[opponentCardIndex];
    setOpponentChoice(opponentCard);

    let outcome = '';
    if (choice === CARD_TYPES.EMPEROR && opponentCard.type === CARD_TYPES.SLAVE) {
      outcome = '玩家失敗!';
      setIsTie(false);
    } else if (choice === CARD_TYPES.SLAVE && opponentCard.type === CARD_TYPES.EMPEROR) {
      outcome = '玩家勝利!';
      setIsTie(false);
    } else if (choice === CARD_TYPES.COMMONER && opponentCard.type === CARD_TYPES.EMPEROR) {
      outcome = '玩家失敗!';
      setIsTie(false);
    } else if (choice === CARD_TYPES.EMPEROR && opponentCard.type === CARD_TYPES.COMMONER) {
      outcome = '玩家勝利!';
      setIsTie(false);
    } else if (choice === CARD_TYPES.COMMONER && opponentCard.type === CARD_TYPES.SLAVE) {
      outcome = '玩家勝利!';
      setIsTie(false);
    } else if (choice === CARD_TYPES.SLAVE && opponentCard.type === CARD_TYPES.COMMONER) {
      outcome = '玩家失敗!';
      setIsTie(false);
    } else {
      outcome = '平局!';
      setIsTie(true);
    }

    setResult({ playerChoice: choice, playerImg: CARD_IMAGES[choice], opponentChoice: opponentCard.img, outcome });

    const updatedPlayerHand = playerHand.filter((_, i) => i !== index);
    const updatedOpponentHand = opponentHand.filter((_, i) => i !== opponentCardIndex);
    setPlayerHand(updatedPlayerHand);
    setOpponentHand(updatedOpponentHand);

    setGameOver(true);
  };

  return (
    <div className="container">
      <h1>E Card Game</h1>
      <div id="game">
        {!gameStarted ? (
          <div id="playerSelection">
            <h2>選擇角色</h2>
            <div className="roleSelection">
              <button id="emperorButton" onClick={() => startGame(CARD_TYPES.EMPEROR)}>
                <img src={CARD_IMAGES[CARD_TYPES.EMPEROR]} alt="皇帝" style={{ maxWidth: '100px' }} />
                <div>皇帝</div>
              </button>
              <button id="slaveButton" onClick={() => startGame(CARD_TYPES.SLAVE)}>
                <img src={CARD_IMAGES[CARD_TYPES.SLAVE]} alt="奴隸" style={{ maxWidth: '100px' }} />
                <div>奴隸</div>
              </button>
            </div>
          </div>
        ) : (
          <>
            {!gameOver ? (
              <div id="playerHand">
                <h2>選擇你的牌</h2>
                {playerHand.map((card, index) => (
                  <button key={index} onClick={() => chooseCard(card.type, index)}>
                    <img src={card.img} alt={card.type} style={{ maxWidth: '100px' }} />
                  </button>
                ))}
              </div>
            ) : (
              <div id="resultScreen">
                <div id="result">
                  {result && (
                    <div>
                      <div className="playerChoice">
                        <h2>玩家出牌: </h2>
                        <img src={result.playerImg} alt={result.playerChoice} style={{ maxWidth: '100px' }} />
                      </div>
                      <div className="opponentChoice">
                        <h2>電腦出牌: </h2>
                        <img src={result.opponentChoice} alt={result.opponentChoice} style={{ maxWidth: '100px' }} />
                      </div>
                      <h2>{result.outcome}</h2>
                    </div>
                  )}
                </div>
                {isTie ? (
                  <button id="continueButton" onClick={continueGame}>繼續</button>
                ) : (
                  <button id="resetButton" onClick={resetGame}>再來一局</button>
                )}
              </div>
            )}
          </>
        )}
      </div>
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById('root'));

