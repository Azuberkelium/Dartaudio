import React, { useState, useEffect, useRef } from 'react';
import { 
  Mic, Square, Play, Trash2, Trophy, Target, 
  RotateCcw, Activity, ChevronLeft, BarChart2, 
  Plus, Check, Bot, ArrowRight, Download, Edit2, Zap
} from 'lucide-react';

// --- Constants & Defaults ---
const STORAGE_KEY_DATA = 'darts_app_data_v5';
const STORAGE_KEY_GAME = 'darts_app_current_game_v5';

const INITIAL_STATS = {
  gamesPlayed: 0,
  wins: 0,
  losses: 0,
  highestCheckout: 0,
  totalDarts: 0,
  totalScore: 0,
  _180s: 0,
  _140s: 0,
  _100s: 0,
};

const BOT_LEVELS = {
  EASY: { name: 'Pub Beginner', avg: 40, checkoutRate: 0.1, color: 'text-green-400' },
  MEDIUM: { name: 'League Captain', avg: 60, checkoutRate: 0.3, color: 'text-yellow-400' },
  HARD: { name: 'PDC Pro', avg: 95, checkoutRate: 0.7, color: 'text-red-500' },
};

const DEFAULT_TRIGGERS = [
  { id: 'def_180', type: 'TURN_SCORE', value: 180, label: 'One Hundred and Eighty!', isDefault: true },
  { id: 'def_win', type: 'EVENT', value: 'win', label: 'Game Shot, and the match!', isDefault: true },
  { id: 'def_bust', type: 'EVENT', value: 'bust', label: 'Bust!', isDefault: true },
  { id: 'def_start', type: 'EVENT', value: 'game_on', label: 'Game On', isDefault: true },
  { id: 'def_botwin', type: 'EVENT', value: 'bot_win', label: 'Bot wins the match', isDefault: true },
  { id: 'def_chips', type: 'SEQUENCE', value: '20,5,1', label: 'Fish and Chips!', isDefault: true },
  { id: 'def_mot1', type: 'MOTIVATION', value: 'focus', label: 'Stay Focused!', isDefault: true },
];

const getCheckoutGuide = (score) => {
  if (score > 170 || score < 2) return null;
  const checkouts = {
    170: 'T20 T20 Bull', 167: 'T20 T19 Bull', 164: 'T20 T18 Bull', 161: 'T20 T17 Bull',
    160: 'T20 T20 D20', 158: 'T20 T20 D19', 156: 'T20 T20 D18', 150: 'T20 T18 D18',
    140: 'T20 T16 D16', 136: 'T20 T20 D8', 132: 'T20 T20 D6', 130: 'T20 T18 D8',
    121: 'T20 T11 D14', 120: 'T20 20 D20', 110: 'T20 10 D20', 100: 'T20 D20',
    90: 'T18 D18', 82: 'T14 D20', 80: 'T20 D10', 70: 'T18 D8', 60: '20 D20',
    50: '10 D20', 40: 'D20', 36: 'D18', 32: 'D16', 20: 'D10', 10: 'D5', 4: 'D2', 2: 'D1'
  };
  return checkouts[score] || null;
};

const speak = (text) => {
  if ('speechSynthesis' in window) {
    window.speechSynthesis.cancel(); 
    const utterance = new SpeechSynthesisUtterance(text);
    utterance.rate = 1.1; 
    window.speechSynthesis.speak(utterance);
  }
};

// --- Main Component ---
export default function App() {
  const [view, setView] = useState('menu'); 
  const [stats, setStats] = useState(INITIAL_STATS);
  const [triggers, setTriggers] = useState(DEFAULT_TRIGGERS);
  const [gameState, setGameState] = useState(null);

  useEffect(() => {
    // Inject JSZip for exporting
    if (!document.getElementById('jszip-script')) {
      const script = document.createElement('script');
      script.id = 'jszip-script';
      script.src = 'https://cdnjs.cloudflare.com/ajax/libs/jszip/3.10.1/jszip.min.js';
      document.body.appendChild(script);
    }

    const savedData = localStorage.getItem(STORAGE_KEY_DATA);
    if (savedData) {
      const parsed = JSON.parse(savedData);
      setStats(parsed.stats || INITIAL_STATS);
      const loadedTriggers = parsed.triggers || [];
      const mergedTriggers = [...DEFAULT_TRIGGERS];
      loadedTriggers.forEach(lt => {
        const index = mergedTriggers.findIndex(mt => mt.id === lt.id);
        if (index >= 0) mergedTriggers[index] = lt;
        else mergedTriggers.push(lt);
      });
      setTriggers(mergedTriggers);
    }

    const savedGame = localStorage.getItem(STORAGE_KEY_GAME);
    if (savedGame) {
      const parsedGame = JSON.parse(savedGame);
      setGameState(parsedGame);
      if (parsedGame.active) {
        setView(parsedGame.type === 'x01' ? 'game_x01' : 'warm_up');
      }
    }
  }, []);

  useEffect(() => {
    localStorage.setItem(STORAGE_KEY_DATA, JSON.stringify({ stats, triggers }));
  }, [stats, triggers]);

  useEffect(() => {
    if (gameState) localStorage.setItem(STORAGE_KEY_GAME, JSON.stringify(gameState));
  }, [gameState]);

  const playTrigger = (type, value) => {
    // Find precise match first
    const match = triggers.find(t => t.type === type && t.value == value);
    
    if (match) {
      if (match.audioData) {
        const audio = new Audio(match.audioData);
        audio.play().catch(e => console.error("Playback failed", e));
      } else {
        speak(match.label);
      }
      return true;
    }
    return false;
  };

  const renderView = () => {
    switch (view) {
      case 'menu': return <MainMenu onNavigate={setView} hasActiveGame={gameState?.active} onContinue={() => setView(gameState.type === 'x01' ? 'game_x01' : 'warm_up')} />;
      case 'game_setup': return <GameSetup onStart={(s, b) => {
        playTrigger('EVENT', 'game_on');
        setGameState({ active: true, type: 'x01', startScore: s, botLevel: b, playerScore: s, botScore: s, turn: 'player', history: [], dartsThrown: 0 });
        setView('game_x01');
      }} onBack={() => setView('menu')} />;
      case 'game_x01': return <X01Game state={gameState} setState={setGameState} stats={stats} setStats={setStats} playTrigger={playTrigger} triggers={triggers} onExit={() => { setGameState({...gameState, active: false}); setView('menu'); }} />;
      case 'warm_up': return <WarmUpGame state={gameState || { active: true, type: 'warmup', target: 1, hits: 0, misses: 0 }} setState={setGameState} onExit={() => setView('menu')} />;
      case 'voice_studio': return <VoiceStudio triggers={triggers} setTriggers={setTriggers} onBack={() => setView('menu')} />;
      case 'stats': return <StatsView stats={stats} onBack={() => setView('menu')} />;
      default: return <MainMenu />;
    }
  };

  return (
    <div className="min-h-screen bg-slate-900 text-slate-100 font-sans selection:bg-emerald-500 selection:text-white">
      <div className="max-w-md mx-auto min-h-screen shadow-2xl bg-slate-900 relative">
        {renderView()}
      </div>
    </div>
  );
}

// -----------------------------------------------------------------------------
// SUB-COMPONENTS
// -----------------------------------------------------------------------------

function MainMenu({ onNavigate, hasActiveGame, onContinue }) {
  return (
    <div className="p-6 flex flex-col h-screen">
      <div className="flex-1 flex flex-col justify-center items-center space-y-8">
        <div className="text-center space-y-2">
          <div className="w-24 h-24 bg-emerald-500 rounded-3xl mx-auto flex items-center justify-center shadow-lg shadow-emerald-500/20 rotate-6 hover:rotate-12 transition-transform">
            <Target size={56} className="text-slate-900" />
          </div>
          <h1 className="text-4xl font-black tracking-tighter text-white">
            PRO SCORER
            <span className="block text-lg font-medium text-emerald-400 tracking-normal">Voice Edition</span>
          </h1>
        </div>
        <div className="w-full space-y-4">
          {hasActiveGame && (
            <button onClick={onContinue} className="w-full p-4 bg-slate-800 border border-emerald-500/30 rounded-xl flex items-center justify-between group hover:bg-slate-700 transition-all animate-pulse-slow">
              <span className="flex items-center font-bold text-emerald-400"><RotateCcw className="mr-3" /> Continue Game</span>
              <ChevronLeft className="rotate-180 group-hover:translate-x-1 transition-transform" />
            </button>
          )}
          <button onClick={() => onNavigate('game_setup')} className="w-full p-5 bg-gradient-to-r from-emerald-600 to-emerald-500 rounded-xl flex items-center justify-between shadow-lg shadow-emerald-500/20 active:scale-95 transition-transform">
            <span className="flex items-center text-xl font-bold text-slate-900"><Play className="mr-3 fill-slate-900" /> Play X01</span>
          </button>
          <button onClick={() => onNavigate('warm_up')} className="w-full p-4 bg-slate-800 rounded-xl flex items-center justify-between hover:bg-slate-700 active:scale-95 transition-transform">
            <span className="flex items-center font-bold text-slate-300"><Activity className="mr-3 text-blue-400" /> Warm Up</span>
          </button>
          <div className="grid grid-cols-2 gap-4">
            <button onClick={() => onNavigate('voice_studio')} className="p-4 bg-slate-800 rounded-xl flex flex-col items-center justify-center hover:bg-slate-700 active:scale-95 transition-all">
              <Mic size={28} className="mb-2 text-rose-400" />
              <span className="text-sm font-bold text-slate-400">Voice Studio</span>
            </button>
            <button onClick={() => onNavigate('stats')} className="p-4 bg-slate-800 rounded-xl flex flex-col items-center justify-center hover:bg-slate-700 active:scale-95 transition-all">
              <BarChart2 size={28} className="mb-2 text-yellow-400" />
              <span className="text-sm font-bold text-slate-400">Stats</span>
            </button>
          </div>
        </div>
      </div>
      <div className="text-center text-slate-600 text-xs py-4">v5.0 • Auto-saving enabled</div>
    </div>
  );
}

function GameSetup({ onStart, onBack }) {
  const [score, setScore] = useState(501);
  const [botLevel, setBotLevel] = useState('MEDIUM');

  return (
    <div className="p-6 h-screen flex flex-col">
      <Header title="New Game" onBack={onBack} />
      <div className="flex-1 space-y-8 mt-4">
        <div className="space-y-3">
          <label className="text-sm font-bold text-slate-400 uppercase tracking-wider">Starting Score</label>
          <div className="grid grid-cols-2 gap-4">
            {[301, 501].map(s => (
              <button key={s} onClick={() => setScore(s)} className={`p-6 rounded-2xl font-black text-2xl border-2 transition-all ${score === s ? 'border-emerald-500 bg-emerald-500/10 text-emerald-400' : 'border-slate-700 bg-slate-800 text-slate-500'}`}>
                {s}
              </button>
            ))}
          </div>
        </div>
        <div className="space-y-3">
          <label className="text-sm font-bold text-slate-400 uppercase tracking-wider">Bot Difficulty</label>
          <div className="space-y-2">
            {Object.keys(BOT_LEVELS).map(key => {
              const level = BOT_LEVELS[key];
              return (
                <button key={key} onClick={() => setBotLevel(key)} className={`w-full p-4 rounded-xl flex items-center justify-between border transition-all ${botLevel === key ? `border-current ${level.color} bg-slate-800` : 'border-transparent bg-slate-800/50 text-slate-500'}`}>
                  <span className="font-bold">{level.name}</span>
                  <span className="text-xs font-mono opacity-60">Avg: {level.avg}</span>
                </button>
              );
            })}
          </div>
        </div>
      </div>
      <button onClick={() => onStart(score, botLevel)} className="w-full py-5 bg-emerald-500 hover:bg-emerald-400 text-slate-900 font-bold text-xl rounded-xl shadow-lg shadow-emerald-500/20 active:scale-95 transition-all">Start Match</button>
    </div>
  );
}

function X01Game({ state, setState, stats, setStats, playTrigger, triggers, onExit }) {
  const [inputMode, setInputMode] = useState('TOTAL'); // 'TOTAL' or 'DARTS'
  const [input, setInput] = useState('');
  const [darts, setDarts] = useState([null, null, null]);
  const [currentDartIdx, setCurrentDartIdx] = useState(0);

  const botConfig = BOT_LEVELS[state.botLevel];
  const checkoutGuide = getCheckoutGuide(state.playerScore);

  useEffect(() => {
    if (state.turn === 'bot' && state.active) {
      const timer = setTimeout(handleBotTurn, 1500 + Math.random() * 1000);
      return () => clearTimeout(timer);
    }
  }, [state.turn, state.active]);

  const handleBotTurn = () => {
    let score = 0;
    const remaining = state.botScore;
    
    // Checkouts
    if (remaining <= 170 && remaining > 1 && ![169,168,165,163,159].includes(remaining)) {
      if (Math.random() < botConfig.checkoutRate) {
        playTrigger('EVENT', 'bot_win');
        finishGame('bot');
        return;
      }
    }
    const variance = 20;
    score = Math.floor(botConfig.avg + (Math.random() * variance * 2) - variance);
    if (score > 180) score = 180;
    if (score < 0) score = 0;
    
    if (remaining - score < 2 && remaining - score !== 0) score = 0;
    else if (remaining - score === 0) {
      playTrigger('EVENT', 'bot_win');
      finishGame('bot');
      return;
    }
    setState(prev => ({
      ...prev,
      botScore: prev.botScore - score,
      turn: 'player',
      history: [...state.history, { player: 'bot', score, remaining: remaining - score }]
    }));
  };

  const playMotivation = () => {
    const motivationClips = triggers.filter(t => t.type === 'MOTIVATION');
    if (motivationClips.length > 0) {
      const randomClip = motivationClips[Math.floor(Math.random() * motivationClips.length)];
      if (randomClip.audioData) new Audio(randomClip.audioData).play();
      else speak(randomClip.label);
    } else {
      speak("You can do it!");
    }
  };

  const handleKeypad = (val) => {
    if (inputMode === 'TOTAL') {
      if (input.length >= 3) return;
      setInput(prev => prev + val);
    } else {
      // Darts Mode
      const currentVal = darts[currentDartIdx] || '';
      if (currentVal.toString().length >= 2 && currentVal !== '25') return; // Max 2 digits mostly
      const newVal = parseInt(currentVal + val, 10);
      if (newVal > 60) return; // Simple sanity check per dart (max T20 = 60)
      
      const newDarts = [...darts];
      newDarts[currentDartIdx] = newVal;
      setDarts(newDarts);
    }
  };

  const nextDart = () => {
    if (currentDartIdx < 2) setCurrentDartIdx(currentDartIdx + 1);
  };

  const backspace = () => {
    if (inputMode === 'TOTAL') {
      setInput(prev => prev.slice(0, -1));
    } else {
      const newDarts = [...darts];
      if (newDarts[currentDartIdx] !== null) {
        const str = newDarts[currentDartIdx].toString();
        if (str.length > 1) newDarts[currentDartIdx] = parseInt(str.slice(0, -1), 10);
        else newDarts[currentDartIdx] = null;
        setDarts(newDarts);
      } else if (currentDartIdx > 0) {
        setCurrentDartIdx(currentDartIdx - 1);
      }
    }
  };

  const submitScore = () => {
    let score = 0;
    let sequence = null;

    if (inputMode === 'TOTAL') {
      score = parseInt(input, 10);
    } else {
      score = darts.reduce((a, b) => a + (b || 0), 0);
      // Filter out nulls for sequence check
      const validDarts = darts.filter(d => d !== null);
      if (validDarts.length === 3) sequence = validDarts.join(',');
    }

    if (isNaN(score)) return;
    if (score > 180) { alert("Max score is 180"); setInput(''); return; }

    const remaining = state.playerScore - score;
    let isWin = remaining === 0;
    let isBust = remaining < 0 || remaining === 1;

    // --- AUDIO LOGIC ---
    let played = false;
    if (isWin) played = playTrigger('EVENT', 'win');
    else if (isBust) played = playTrigger('EVENT', 'bust');
    else {
      // Priority 0: SEQUENCE (e.g., 20,5,1)
      if (sequence) {
        played = playTrigger('SEQUENCE', sequence);
      }
      
      // Priority 1: Check Remaining
      if (!played) played = playTrigger('REMAINING_SCORE', remaining);
      
      // Priority 2: Check Turn Score
      if (!played) played = playTrigger('TURN_SCORE', score);
    }
    // -------------------

    if (!isBust) {
      const newStats = { ...stats, totalScore: stats.totalScore + score, totalDarts: stats.totalDarts + 3 };
      if (score === 180) newStats._180s++;
      else if (score >= 140) newStats._140s++;
      else if (score >= 100) newStats._100s++;
      if (isWin) {
        newStats.gamesPlayed++;
        newStats.wins++;
        if (score > newStats.highestCheckout) newStats.highestCheckout = score;
        setStats(newStats);
        finishGame('player');
        return;
      }
      setStats(newStats);
    }

    setState(prev => ({
      ...prev,
      playerScore: isBust ? prev.playerScore : remaining,
      turn: 'bot',
      history: [...prev.history, { player: 'player', score: isBust ? 0 : score, remaining: isBust ? prev.playerScore : remaining }]
    }));
    setInput('');
    setDarts([null, null, null]);
    setCurrentDartIdx(0);
  };

  const finishGame = (winner) => {
    if (winner === 'bot') {
       setStats(prev => ({ ...prev, gamesPlayed: prev.gamesPlayed + 1, losses: prev.losses + 1 }));
    }
    setState(prev => ({ ...prev, active: false, winner }));
  };

  if (!state.active && state.winner) {
    return (
      <div className="h-screen flex flex-col items-center justify-center p-6 space-y-6 text-center bg-slate-900">
        {state.winner === 'player' ? <Trophy size={80} className="text-emerald-400 animate-bounce" /> : <Target size={80} className="text-red-400" />}
        <h2 className="text-5xl font-black text-white">{state.winner === 'player' ? 'VICTORY' : 'DEFEAT'}</h2>
        <button onClick={onExit} className="w-full py-4 bg-slate-700 rounded-xl font-bold text-white mt-8">Back to Menu</button>
      </div>
    );
  }

  return (
    <div className="h-screen flex flex-col bg-slate-900">
      <div className="flex-none p-4 grid grid-cols-2 gap-4 border-b border-slate-800">
        <div className={`p-4 rounded-2xl flex flex-col items-center transition-all ${state.turn === 'player' ? 'bg-slate-800 border-2 border-emerald-500 scale-105' : 'bg-slate-900 border border-slate-800 opacity-60'}`}>
          <span className="text-xs font-bold text-slate-400 uppercase">You</span>
          <span className="text-6xl font-black text-white">{state.playerScore}</span>
          {checkoutGuide && state.turn === 'player' && <span className="text-xs text-emerald-400 font-mono mt-2">{checkoutGuide}</span>}
        </div>
        <div className={`p-4 rounded-2xl flex flex-col items-center transition-all ${state.turn === 'bot' ? 'bg-slate-800 border-2 border-red-500 scale-105' : 'bg-slate-900 border border-slate-800 opacity-60'}`}>
          <span className="text-xs font-bold text-slate-400 uppercase">{botConfig.name}</span>
          <span className="text-6xl font-black text-white">{state.botScore}</span>
        </div>
      </div>

      <div className="flex-1 overflow-y-auto p-4 space-y-2 bg-slate-900/50">
        {state.history.slice().reverse().map((h, i) => (
          <div key={i} className="flex justify-between text-xs text-slate-500 border-b border-slate-800 pb-1">
            <span className={h.player === 'player' ? 'text-emerald-500 font-bold' : ''}>{h.player === 'player' ? 'YOU' : 'BOT'}</span>
            <span>Scored: {h.score}</span>
            <span>Left: {h.remaining}</span>
          </div>
        ))}
      </div>

      <div className="flex-none bg-slate-800 p-4 rounded-t-3xl shadow-2xl relative">
        {/* Input Mode Tabs & Motivation */}
        <div className="flex justify-center items-center -mt-8 mb-4 space-x-2">
             <div className="bg-slate-900 p-1 rounded-xl flex shadow-lg">
                <button 
                  onClick={() => setInputMode('TOTAL')} 
                  className={`px-4 py-2 rounded-lg text-xs font-bold transition-all ${inputMode === 'TOTAL' ? 'bg-emerald-500 text-slate-900' : 'text-slate-400 hover:text-white'}`}
                >
                  Total Score
                </button>
                <button 
                  onClick={() => setInputMode('DARTS')} 
                  className={`px-4 py-2 rounded-lg text-xs font-bold transition-all ${inputMode === 'DARTS' ? 'bg-blue-500 text-white' : 'text-slate-400 hover:text-white'}`}
                >
                  Dart by Dart
                </button>
             </div>
             <button onClick={playMotivation} className="h-10 w-10 bg-yellow-400 rounded-xl flex items-center justify-center shadow-lg hover:bg-yellow-300 active:scale-95 transition-all" title="Play Motivation">
                <Zap size={20} className="text-slate-900 fill-slate-900" />
             </button>
        </div>

        {/* Display Area */}
        <div className="flex justify-center mb-4 h-16 items-center">
          {state.turn === 'player' ? (
             inputMode === 'TOTAL' ? (
                <div className="text-5xl font-mono font-bold text-emerald-400 tracking-widest">{input || <span className="opacity-20">0</span>}</div>
             ) : (
                <div className="flex space-x-3">
                   {[0,1,2].map(idx => (
                      <div key={idx} 
                           onClick={() => setCurrentDartIdx(idx)}
                           className={`w-14 h-14 rounded-full flex items-center justify-center text-xl font-bold border-2 transition-all cursor-pointer
                           ${currentDartIdx === idx ? 'border-blue-500 bg-blue-500/20 text-blue-400 scale-110 shadow-lg shadow-blue-500/20' : 'border-slate-700 bg-slate-900 text-slate-500'}`}>
                         {darts[idx] !== null ? darts[idx] : '-'}
                      </div>
                   ))}
                   <div className="w-14 h-14 rounded-lg flex flex-col items-center justify-center bg-slate-900 border border-slate-700">
                      <span className="text-[10px] text-slate-500 uppercase">Total</span>
                      <span className="text-lg font-bold text-white">{darts.reduce((a,b) => a+(b||0), 0)}</span>
                   </div>
                </div>
             )
          ) : (
            <span className="text-slate-500 animate-pulse mt-2">Opponent throwing...</span>
          )}
        </div>

        {/* Keypad */}
        <div className="grid grid-cols-4 gap-3 max-w-sm mx-auto">
          {[1,2,3].map(n => <KeyBtn key={n} n={n} onClick={() => handleKeypad(n.toString())} disabled={state.turn === 'bot'} />)}
          <button disabled={state.turn === 'bot'} onClick={backspace} className="h-14 rounded-lg bg-slate-700/50 text-red-400 flex items-center justify-center disabled:opacity-30"><RotateCcw size={20} /></button>
          
          {[4,5,6].map(n => <KeyBtn key={n} n={n} onClick={() => handleKeypad(n.toString())} disabled={state.turn === 'bot'} />)}
          <button disabled={state.turn === 'bot'} onClick={() => { if(inputMode === 'DARTS') nextDart(); }} className={`h-14 rounded-lg flex items-center justify-center disabled:opacity-30 ${inputMode === 'DARTS' ? 'bg-slate-700 text-blue-400' : 'bg-slate-800 text-slate-600'}`}>
             {inputMode === 'DARTS' ? <ArrowRight size={24} /> : <div className="w-2 h-2 rounded-full bg-slate-700" />}
          </button>

          {[7,8,9,0].map(n => <KeyBtn key={n} n={n} onClick={() => handleKeypad(n.toString())} disabled={state.turn === 'bot'} />)}
        </div>
        
        <button disabled={state.turn === 'bot' || (inputMode === 'TOTAL' && !input) || (inputMode === 'DARTS' && darts.every(d => d === null))} onClick={submitScore} className={`w-full mt-3 h-14 rounded-lg font-bold text-xl flex items-center justify-center disabled:opacity-30 active:scale-95 transition-transform shadow-lg ${inputMode === 'TOTAL' ? 'bg-emerald-500 text-slate-900 shadow-emerald-500/20' : 'bg-blue-500 text-white shadow-blue-500/20'}`}>
          {inputMode === 'TOTAL' ? 'ENTER SCORE' : 'ENTER 3 DARTS'}
        </button>
        <button onClick={onExit} className="w-full mt-3 text-xs text-slate-500 uppercase tracking-widest font-bold hover:text-white">Exit Game</button>
      </div>
    </div>
  );
}

const KeyBtn = ({ n, onClick, disabled }) => (
    <button disabled={disabled} onClick={onClick} className="h-14 rounded-lg bg-slate-700 text-white text-xl font-bold active:bg-slate-600 disabled:opacity-30">{n}</button>
);

function WarmUpGame({ state, setState, onExit }) {
  const currentTarget = state.target;
  const handleHit = () => {
    if (currentTarget === 25) { alert("Warm up complete!"); onExit(); } 
    else setState(prev => ({ ...prev, target: prev.target === 20 ? 25 : prev.target + 1, hits: prev.hits + 1 }));
  };
  const handleMiss = () => setState(prev => ({ ...prev, misses: prev.misses + 1 }));

  return (
    <div className="h-screen flex flex-col p-6 bg-slate-900">
      <Header title="Warm Up" onBack={onExit} />
      <div className="flex-1 flex flex-col items-center justify-center space-y-8">
        <div className="text-center">
          <p className="text-slate-400 font-bold uppercase tracking-widest mb-2">Aim For</p>
          <div className="text-9xl font-black text-emerald-400 drop-shadow-[0_0_30px_rgba(52,211,153,0.3)]">{currentTarget === 25 ? 'BULL' : currentTarget}</div>
        </div>
        <div className="grid grid-cols-2 gap-8 w-full max-w-xs">
          <button onClick={handleMiss} className="aspect-square rounded-2xl bg-slate-800 border-2 border-slate-700 flex flex-col items-center justify-center text-slate-400 hover:bg-slate-700"><span className="text-3xl font-black mb-1">MISS</span></button>
          <button onClick={handleHit} className="aspect-square rounded-2xl bg-emerald-500 text-slate-900 flex flex-col items-center justify-center hover:bg-emerald-400"><span className="text-3xl font-black mb-1">HIT</span></button>
        </div>
      </div>
    </div>
  );
}

// --- Voice Studio with Export ---
function VoiceStudio({ triggers, setTriggers, onBack }) {
  const [mode, setMode] = useState('list');
  const [editingId, setEditingId] = useState(null);

  const [newType, setNewType] = useState('TURN_SCORE');
  const [newValue, setNewValue] = useState('');
  const [newLabel, setNewLabel] = useState('');
  const [recording, setRecording] = useState(false);
  const [tempAudio, setTempAudio] = useState(null);
  const recorderRef = useRef(null);
  const chunksRef = useRef([]);

  const startRec = async () => {
    try {
      const stream = await navigator.mediaDevices.getUserMedia({ audio: true });
      let mimeType = 'audio/webm';
      if (MediaRecorder.isTypeSupported('audio/mp4')) mimeType = 'audio/mp4';
      
      const rec = new MediaRecorder(stream, { mimeType });
      chunksRef.current = [];
      rec.ondataavailable = e => chunksRef.current.push(e.data);
      rec.onstop = () => {
        const blob = new Blob(chunksRef.current, { type: mimeType });
        const reader = new FileReader();
        reader.readAsDataURL(blob);
        reader.onloadend = () => setTempAudio(reader.result);
        stream.getTracks().forEach(t => t.stop());
      };
      rec.start();
      recorderRef.current = rec;
      setRecording(true);
    } catch(e) { alert("Mic error: Check permissions"); }
  };

  const stopRec = () => {
    if (recorderRef.current) {
      recorderRef.current.stop();
      setRecording(false);
    }
  };

  const editTrigger = (t) => {
    setEditingId(t.id);
    setNewType(t.type);
    setNewValue(t.value);
    setNewLabel(t.label);
    setTempAudio(t.audioData);
    setMode('create');
  };

  const saveTrigger = () => {
    // Value is required unless it's motivation mode (we auto-generate it)
    let valToSave = newValue;
    if (newType === 'MOTIVATION' && !valToSave) {
        valToSave = `mot_${Date.now()}`;
    }
    
    if (!valToSave) return;
    
    // Construct new object
    const triggerData = {
      type: newType,
      value: valToSave,
      label: newLabel || (newType === 'SEQUENCE' ? `Combo: ${valToSave}` : (newType === 'MOTIVATION' ? 'Motivational Clip' : `${newType === 'TURN_SCORE' ? 'Scored' : 'Left'} ${valToSave}`)),
      audioData: tempAudio,
      isDefault: false
    };

    if (editingId) {
      // Update existing
      setTriggers(prev => prev.map(t => t.id === editingId ? { ...t, ...triggerData } : t));
    } else {
      // Create new
      const newTrigger = { ...triggerData, id: Date.now().toString() };
      setTriggers(prev => [...prev, newTrigger]);
    }

    // Reset Form
    setMode('list');
    setEditingId(null);
    setTempAudio(null);
    setNewValue('');
    setNewLabel('');
  };

  const cancelEdit = () => {
    setMode('list');
    setEditingId(null);
    setTempAudio(null);
    setNewValue('');
    setNewLabel('');
  };

  const deleteTrigger = (id) => {
    if(window.confirm("Delete this recording?")) {
      setTriggers(triggers.filter(t => t.id !== id));
    }
  };

  const testTrigger = (t) => {
    if (t.audioData) new Audio(t.audioData).play();
    else speak(t.label);
  };

  const downloadAll = () => {
    if (typeof window.JSZip === 'undefined') {
       alert("Export library is loading, please try again in a few seconds.");
       return;
    }
    const zip = new window.JSZip();
    const folder = zip.folder("dart_voice_recordings");
    
    let count = 0;
    triggers.forEach(t => {
      if (t.audioData) {
        const parts = t.audioData.split(',');
        const ext = parts[0].includes('mp4') ? 'mp4' : 'webm';
        const filename = `${t.label.replace(/[^a-z0-9]/gi, '_')}.${ext}`;
        folder.file(filename, parts[1], {base64: true});
        count++;
      }
    });

    if (count === 0) {
      alert("No custom recordings found to export.");
      return;
    }

    zip.generateAsync({type:"blob"}).then(function(content) {
        const link = document.createElement("a");
        link.href = URL.createObjectURL(content);
        link.download = "dart_voices.zip";
        link.click();
    });
  };

  if (mode === 'create') {
    return (
      <div className="h-screen flex flex-col p-6 bg-slate-900">
        <Header title={editingId ? "Edit Trigger" : "New Voice Trigger"} onBack={cancelEdit} />
        <div className="space-y-6 mt-4">
          <div className="space-y-2">
            <label className="text-xs font-bold text-slate-500 uppercase">Category</label>
            <div className="grid grid-cols-2 gap-2">
              <button onClick={() => setNewType('TURN_SCORE')} className={`p-3 rounded-lg text-xs font-bold border ${newType === 'TURN_SCORE' ? 'bg-emerald-500/20 border-emerald-500 text-emerald-400' : 'bg-slate-800 border-slate-700 text-slate-400'}`}>I Scored...</button>
              <button onClick={() => setNewType('REMAINING_SCORE')} className={`p-3 rounded-lg text-xs font-bold border ${newType === 'REMAINING_SCORE' ? 'bg-blue-500/20 border-blue-500 text-blue-400' : 'bg-slate-800 border-slate-700 text-slate-400'}`}>I Have Left...</button>
              <button onClick={() => setNewType('SEQUENCE')} className={`p-3 rounded-lg text-xs font-bold border ${newType === 'SEQUENCE' ? 'bg-orange-500/20 border-orange-500 text-orange-400' : 'bg-slate-800 border-slate-700 text-slate-400'}`}>Dart Sequence</button>
              <button onClick={() => setNewType('EVENT')} className={`p-3 rounded-lg text-xs font-bold border ${newType === 'EVENT' ? 'bg-purple-500/20 border-purple-500 text-purple-400' : 'bg-slate-800 border-slate-700 text-slate-400'}`}>Game Event</button>
            </div>
            <button onClick={() => setNewType('MOTIVATION')} className={`w-full mt-2 p-3 rounded-lg text-xs font-bold border ${newType === 'MOTIVATION' ? 'bg-yellow-500/20 border-yellow-500 text-yellow-400' : 'bg-slate-800 border-slate-700 text-slate-400'}`}>Motivation</button>
          </div>

          {newType !== 'MOTIVATION' && (
            <div className="space-y-2">
               <label className="text-xs font-bold text-slate-500 uppercase">
                  {newType === 'TURN_SCORE' && "Turn Score (e.g. 180, 26)"}
                  {newType === 'REMAINING_SCORE' && "Score Remaining (e.g. 32, 170)"}
                  {newType === 'SEQUENCE' && "Exact Sequence (e.g. 20,5,1)"}
                  {newType === 'EVENT' && "Select Event"}
               </label>
               {newType === 'EVENT' ? (
                 <select value={newValue} onChange={(e) => setNewValue(e.target.value)} className="w-full p-4 bg-slate-800 rounded-xl text-white outline-none border border-slate-700">
                    <option value="">Select an Event</option>
                    <option value="win">Match Win</option>
                    <option value="bust">Bust</option>
                    <option value="game_on">Game On</option>
                    <option value="bot_win">Bot Wins</option>
                 </select>
               ) : (
                 <input 
                  type={newType === 'SEQUENCE' ? "text" : "number"}
                  value={newValue} 
                  onChange={e => setNewValue(e.target.value)}
                  placeholder={newType === 'SEQUENCE' ? "20,5,1" : "0"}
                  className="w-full p-4 bg-slate-800 rounded-xl text-white text-2xl font-mono outline-none border focus:border-emerald-500 border-slate-700" 
                />
               )}
            </div>
          )}

          <div className="space-y-2">
             <label className="text-xs font-bold text-slate-500 uppercase">Label / Description</label>
             <input value={newLabel} onChange={e => setNewLabel(e.target.value)} placeholder={newType === 'MOTIVATION' ? "e.g. 'Come on!'" : "e.g. 'Fish and Chips'"} className="w-full p-3 bg-slate-800 rounded-lg text-white" />
          </div>

          <div className="bg-slate-800 p-6 rounded-2xl flex flex-col items-center justify-center space-y-4 border border-slate-700">
            {recording ? (
              <button onClick={stopRec} className="w-20 h-20 bg-red-500 rounded-full animate-pulse flex items-center justify-center shadow-[0_0_30px_rgba(239,68,68,0.4)]">
                <Square fill="white" size={32} />
              </button>
            ) : (
              <button onClick={startRec} className="w-20 h-20 bg-slate-700 rounded-full flex items-center justify-center hover:bg-slate-600 transition-colors">
                <Mic className="text-white" size={32} />
              </button>
            )}
            <p className="text-xs text-slate-500">{recording ? 'Recording...' : tempAudio ? 'Recording Saved!' : 'Tap to Record'}</p>
            {tempAudio && <button onClick={() => new Audio(tempAudio).play()} className="flex items-center text-emerald-400 text-sm font-bold"><Play size={16} className="mr-2"/> Preview Sound</button>}
          </div>

          <button onClick={saveTrigger} disabled={newType !== 'MOTIVATION' && !newValue} className="w-full py-4 bg-emerald-500 text-slate-900 font-bold rounded-xl disabled:opacity-50 disabled:cursor-not-allowed">
            {editingId ? "Update Trigger" : "Save Trigger"}
          </button>
        </div>
      </div>
    );
  }

  return (
    <div className="h-screen flex flex-col p-6 bg-slate-900 overflow-hidden">
      <Header title="Voice Studio" onBack={onBack} />
      
      <div className="mb-4 flex items-center justify-between">
        <span className="text-xs font-bold text-slate-500 uppercase">Library</span>
        <div className="flex space-x-2">
           <button onClick={downloadAll} className="flex items-center text-xs font-bold text-blue-400 bg-blue-500/10 px-3 py-2 rounded-lg hover:bg-blue-500/20">
             <Download size={14} className="mr-1" /> Export All
           </button>
           <button onClick={() => { setEditingId(null); setMode('create'); }} className="flex items-center text-xs font-bold text-emerald-400 bg-emerald-500/10 px-3 py-2 rounded-lg hover:bg-emerald-500/20">
             <Plus size={14} className="mr-1" /> New Trigger
           </button>
        </div>
      </div>

      <div className="flex-1 overflow-y-auto space-y-3 pb-20">
        {triggers.map(trigger => (
          <div key={trigger.id} className="bg-slate-800 p-4 rounded-xl flex items-center justify-between border border-slate-700/50">
            <div className="flex-1">
              <div className="font-bold text-slate-200">{trigger.label}</div>
              <div className="text-xs text-slate-500 flex items-center mt-1 flex-wrap gap-1">
                 {trigger.type === 'TURN_SCORE' && <span className="bg-emerald-500/20 text-emerald-400 px-2 py-0.5 rounded text-[10px]">SCORED {trigger.value}</span>}
                 {trigger.type === 'REMAINING_SCORE' && <span className="bg-blue-500/20 text-blue-400 px-2 py-0.5 rounded text-[10px]">LEFT {trigger.value}</span>}
                 {trigger.type === 'SEQUENCE' && <span className="bg-orange-500/20 text-orange-400 px-2 py-0.5 rounded text-[10px]">SEQ: {trigger.value}</span>}
                 {trigger.type === 'EVENT' && <span className="bg-purple-500/20 text-purple-400 px-2 py-0.5 rounded text-[10px]">EVENT</span>}
                 {trigger.type === 'MOTIVATION' && <span className="bg-yellow-500/20 text-yellow-400 px-2 py-0.5 rounded text-[10px]">MOTIVATION</span>}
                 {trigger.audioData ? 
                   <span className="text-emerald-500 flex items-center text-[10px] ml-1"><Check size={10} className="mr-1"/> Audio</span> : 
                   <span className="text-slate-500 flex items-center text-[10px] ml-1"><Bot size={10} className="mr-1"/> TTS</span>
                 }
              </div>
            </div>
            <div className="flex items-center space-x-2 ml-2">
              <button onClick={() => testTrigger(trigger)} className="p-2 bg-slate-700 rounded-lg text-emerald-400 hover:bg-slate-600"><Play size={16} /></button>
              <button onClick={() => editTrigger(trigger)} className="p-2 bg-slate-700 rounded-lg text-blue-400 hover:bg-slate-600"><Edit2 size={16} /></button>
              {!trigger.isDefault && <button onClick={() => deleteTrigger(trigger.id)} className="p-2 bg-slate-700 rounded-lg text-red-400 hover:bg-slate-600"><Trash2 size={16} /></button>}
            </div>
          </div>
        ))}
      </div>
    </div>
  );
}

function StatsView({ stats, onBack }) {
  const avg = stats.totalDarts > 0 ? ((stats.totalScore / stats.totalDarts) * 3).toFixed(1) : '0.0';
  const winRate = stats.gamesPlayed > 0 ? Math.round((stats.wins / stats.gamesPlayed) * 100) : 0;
  return (
    <div className="h-screen flex flex-col p-6 bg-slate-900 overflow-y-auto">
      <Header title="Career Stats" onBack={onBack} />
      <div className="grid grid-cols-2 gap-4 mt-6">
        <StatCard label="Matches" value={stats.gamesPlayed} />
        <StatCard label="Win Rate" value={`${winRate}%`} sub={`W: ${stats.wins} L: ${stats.losses}`} />
        <StatCard label="3-Dart Avg" value={avg} highlight />
        <StatCard label="Best Checkout" value={stats.highestCheckout} />
      </div>
      <h3 className="text-slate-500 font-bold uppercase tracking-widest mt-8 mb-4 text-sm">Milestones</h3>
      <div className="space-y-3">
        <MilestoneRow label="180s" value={stats._180s} color="text-emerald-400" />
        <MilestoneRow label="140s" value={stats._140s} color="text-slate-300" />
        <MilestoneRow label="Tons (100+)" value={stats._100s} color="text-slate-400" />
      </div>
       <div className="mt-auto pt-8 text-center"><button onClick={() => { if(window.confirm('Reset all stats?')) localStorage.clear(); window.location.reload();}} className="text-xs text-red-500 underline">Reset Data</button></div>
    </div>
  );
}

const Header = ({ title, onBack }) => (
  <div className="flex items-center space-x-4 mb-4">
    <button onClick={onBack} className="p-2 -ml-2 rounded-full hover:bg-slate-800 transition-colors"><ChevronLeft /></button>
    <h2 className="text-xl font-bold text-white">{title}</h2>
  </div>
);

const StatCard = ({ label, value, sub, highlight }) => (
  <div className={`p-4 rounded-2xl bg-slate-800 border ${highlight ? 'border-emerald-500/50' : 'border-slate-800'}`}>
    <div className="text-xs text-slate-500 font-bold uppercase mb-1">{label}</div>
    <div className={`text-2xl font-black ${highlight ? 'text-emerald-400' : 'text-white'}`}>{value}</div>
    {sub && <div className="text-xs text-slate-400 mt-1">{sub}</div>}
  </div>
);

const MilestoneRow = ({ label, value, color }) => (
  <div className="flex items-center justify-between p-4 bg-slate-800 rounded-xl">
    <span className="font-bold text-slate-300">{label}</span>
    <span className={`font-mono font-bold text-xl ${color}`}>{value}</span>
  </div>
);


