import { useState, useEffect, useCallback } from "react";

// Precise math using integer arithmetic to avoid floating-point errors
function preciseMath(a, op, b) {
  const factor = Math.pow(10, 10);
  const fa = Math.round(a * factor);
  const fb = Math.round(b * factor);
  switch (op) {
    case "+": return (fa + fb) / factor;
    case "−": return (fa - fb) / factor;
    case "×": return (fa * fb) / (factor * factor);
    case "÷":
      if (b === 0) return "ERR";
      return fa / fb;
    default: return b;
  }
}

function formatDisplay(val) {
  if (val === "ERR") return "ERR";
  const num = parseFloat(val);
  if (isNaN(num)) return "0";
  // Use toPrecision to avoid floating-point display noise
  const str = parseFloat(num.toPrecision(10)).toString();
  if (str.length > 12) {
    return parseFloat(num.toExponential(5)).toString();
  }
  return str;
}

const BUTTONS = [
  { label: "C",   type: "fn",      wide: false },
  { label: "+/-", type: "fn",      wide: false },
  { label: "%",   type: "fn",      wide: false },
  { label: "÷",   type: "op",      wide: false },
  { label: "7",   type: "num",     wide: false },
  { label: "8",   type: "num",     wide: false },
  { label: "9",   type: "num",     wide: false },
  { label: "×",   type: "op",      wide: false },
  { label: "4",   type: "num",     wide: false },
  { label: "5",   type: "num",     wide: false },
  { label: "6",   type: "num",     wide: false },
  { label: "−",   type: "op",      wide: false },
  { label: "1",   type: "num",     wide: false },
  { label: "2",   type: "num",     wide: false },
  { label: "3",   type: "num",     wide: false },
  { label: "+",   type: "op",      wide: false },
  { label: "⌫",   type: "fn",      wide: false },
  { label: "0",   type: "num",     wide: false },
  { label: ".",   type: "num",     wide: false },
  { label: "=",   type: "eq",      wide: false },
];

export default function Calculator() {
  const [display, setDisplay] = useState("0");
  const [prev, setPrev] = useState(null);
  const [op, setOp] = useState(null);
  const [waitingForOperand, setWaitingForOperand] = useState(false);
  const [justEvaled, setJustEvaled] = useState(false);
  const [activeKey, setActiveKey] = useState(null);
  const [expression, setExpression] = useState("");

  const flash = (key) => {
    setActiveKey(key);
    setTimeout(() => setActiveKey(null), 120);
  };

  const inputDigit = useCallback((digit) => {
    flash(digit);
    if (waitingForOperand || justEvaled) {
      setDisplay(digit === "." ? "0." : digit);
      setWaitingForOperand(false);
      setJustEvaled(false);
    } else {
      if (digit === "." && display.includes(".")) return;
      setDisplay(display === "0" && digit !== "." ? digit : display + digit);
    }
  }, [display, waitingForOperand, justEvaled]);

  const inputOp = useCallback((operator) => {
    flash(operator);
    const current = parseFloat(display);
    if (prev !== null && !waitingForOperand && !justEvaled) {
      const result = preciseMath(prev, op, current);
      if (result === "ERR") {
        setDisplay("ERR"); setPrev(null); setOp(null);
        setExpression(""); setWaitingForOperand(true);
        return;
      }
      const formatted = formatDisplay(result);
      setDisplay(formatted);
      setPrev(parseFloat(formatted));
      setExpression(formatDisplay(result) + " " + operator);
    } else {
      setPrev(current);
      setExpression(formatDisplay(current) + " " + operator);
    }
    setOp(operator);
    setWaitingForOperand(true);
    setJustEvaled(false);
  }, [display, prev, op, waitingForOperand, justEvaled]);

  const evaluate = useCallback(() => {
    flash("=");
    if (op === null || prev === null) return;
    const current = parseFloat(display);
    const result = preciseMath(prev, op, current);
    if (result === "ERR") {
      setDisplay("ERR"); setPrev(null); setOp(null);
      setExpression(""); setWaitingForOperand(true); return;
    }
    const formatted = formatDisplay(result);
    setExpression(formatDisplay(prev) + " " + op + " " + formatDisplay(current) + " =");
    setDisplay(formatted);
    setPrev(null);
    setOp(null);
    setWaitingForOperand(false);
    setJustEvaled(true);
  }, [display, prev, op]);

  const handleFn = useCallback((fn) => {
    flash(fn);
    if (fn === "C") {
      setDisplay("0"); setPrev(null); setOp(null);
      setWaitingForOperand(false); setJustEvaled(false); setExpression("");
    } else if (fn === "+/-") {
      setDisplay(formatDisplay(parseFloat(display) * -1));
    } else if (fn === "%") {
      setDisplay(formatDisplay(parseFloat(display) / 100));
    } else if (fn === "⌫") {
      if (display.length === 1 || (display.length === 2 && display[0] === "-")) {
        setDisplay("0");
      } else {
        setDisplay(display.slice(0, -1));
      }
    }
  }, [display]);

  const handleButton = useCallback((label, type) => {
    if (type === "num") inputDigit(label);
    else if (type === "op") inputOp(label);
    else if (type === "eq") evaluate();
    else handleFn(label);
  }, [inputDigit, inputOp, evaluate, handleFn]);

  // Keyboard support
  useEffect(() => {
    const map = {
      "0":"0","1":"1","2":"2","3":"3","4":"4","5":"5","6":"6","7":"7","8":"8","9":"9",
      ".":".","Enter":"=","=":"=","Backspace":"⌫","Escape":"C",
      "+":"+","-":"−","*":"×","/":"÷","%":"%"
    };
    const handler = (e) => {
      const k = map[e.key];
      if (!k) return;
      e.preventDefault();
      if (["+","−","×","÷"].includes(k)) inputOp(k);
      else if (k === "=") evaluate();
      else if (k === "C") handleFn("C");
      else if (k === "⌫") handleFn("⌫");
      else if (k === "%") handleFn("%");
      else inputDigit(k);
    };
    window.addEventListener("keydown", handler);
    return () => window.removeEventListener("keydown", handler);
  }, [inputDigit, inputOp, evaluate, handleFn]);

  const displayLen = display.length;
  const fontSize = displayLen > 10 ? "text-3xl" : displayLen > 7 ? "text-4xl" : "text-5xl";

  return (
    <div style={{
      minHeight: "100vh",
      background: "radial-gradient(ellipse at 20% 50%, #0f1a2e 0%, #070d1a 40%, #000510 100%)",
      display: "flex",
      alignItems: "center",
      justifyContent: "center",
      fontFamily: "'DM Mono', 'Courier New', monospace",
      position: "relative",
      overflow: "hidden",
    }}>
      {/* Background orbs */}
      <div style={{
        position: "absolute", width: 400, height: 400, borderRadius: "50%",
        background: "radial-gradient(circle, rgba(0,200,180,0.07) 0%, transparent 70%)",
        top: "10%", left: "5%", filter: "blur(40px)", pointerEvents: "none"
      }}/>
      <div style={{
        position: "absolute", width: 300, height: 300, borderRadius: "50%",
        background: "radial-gradient(circle, rgba(100,80,255,0.06) 0%, transparent 70%)",
        bottom: "10%", right: "5%", filter: "blur(40px)", pointerEvents: "none"
      }}/>

      <style>{`
        @import url('https://fonts.googleapis.com/css2?family=DM+Mono:wght@300;400;500&family=Outfit:wght@300;400;600&display=swap');

        * { box-sizing: border-box; margin: 0; padding: 0; }

        .calc-shell {
          background: rgba(255,255,255,0.03);
          backdrop-filter: blur(30px);
          -webkit-backdrop-filter: blur(30px);
          border: 1px solid rgba(255,255,255,0.07);
          border-radius: 32px;
          padding: 28px 24px 24px;
          width: 340px;
          box-shadow:
            0 40px 80px rgba(0,0,0,0.6),
            0 0 0 1px rgba(255,255,255,0.04) inset,
            0 1px 0 rgba(255,255,255,0.1) inset;
        }

        .display-area {
          padding: 16px 12px 20px;
          text-align: right;
          min-height: 110px;
          display: flex;
          flex-direction: column;
          justify-content: flex-end;
          gap: 4px;
        }

        .expression-text {
          font-family: 'DM Mono', monospace;
          font-size: 13px;
          color: rgba(0,220,200,0.45);
          letter-spacing: 0.05em;
          min-height: 18px;
          transition: all 0.2s ease;
          overflow: hidden;
          text-overflow: ellipsis;
          white-space: nowrap;
        }

        .display-text {
          font-family: 'DM Mono', monospace;
          font-weight: 300;
          color: #e8f4f0;
          letter-spacing: -0.02em;
          line-height: 1;
          transition: font-size 0.15s ease;
          overflow: hidden;
          text-overflow: ellipsis;
          white-space: nowrap;
        }

        .display-text.err {
          color: #ff6b6b;
        }

        .divider {
          height: 1px;
          background: linear-gradient(90deg, transparent, rgba(0,220,200,0.15), transparent);
          margin-bottom: 20px;
        }

        .btn-grid {
          display: grid;
          grid-template-columns: repeat(4, 1fr);
          gap: 10px;
        }

        .btn {
          aspect-ratio: 1;
          border: none;
          border-radius: 18px;
          cursor: pointer;
          font-family: 'DM Mono', monospace;
          font-size: 18px;
          font-weight: 400;
          transition: transform 0.1s ease, box-shadow 0.15s ease, background 0.15s ease;
          position: relative;
          overflow: hidden;
          user-select: none;
          -webkit-tap-highlight-color: transparent;
        }

        .btn::before {
          content: '';
          position: absolute;
          inset: 0;
          border-radius: inherit;
          background: linear-gradient(135deg, rgba(255,255,255,0.12) 0%, transparent 60%);
          pointer-events: none;
        }

        .btn:active, .btn.active {
          transform: scale(0.91);
        }

        .btn-num {
          background: rgba(255,255,255,0.06);
          color: #c8ddd8;
          border: 1px solid rgba(255,255,255,0.08);
          box-shadow: 0 4px 12px rgba(0,0,0,0.3), 0 1px 0 rgba(255,255,255,0.07) inset;
        }
        .btn-num:hover { background: rgba(255,255,255,0.1); box-shadow: 0 6px 18px rgba(0,0,0,0.35); }
        .btn-num.active { background: rgba(255,255,255,0.04); box-shadow: 0 2px 6px rgba(0,0,0,0.3); }

        .btn-op {
          background: rgba(0,210,185,0.12);
          color: #00d4b8;
          border: 1px solid rgba(0,210,185,0.2);
          box-shadow: 0 4px 14px rgba(0,210,185,0.1), 0 1px 0 rgba(0,210,185,0.15) inset;
          font-size: 20px;
        }
        .btn-op:hover { background: rgba(0,210,185,0.18); box-shadow: 0 6px 20px rgba(0,210,185,0.15); }
        .btn-op.active { background: rgba(0,210,185,0.08); }

        .btn-fn {
          background: rgba(255,255,255,0.09);
          color: rgba(200,220,215,0.7);
          border: 1px solid rgba(255,255,255,0.1);
          box-shadow: 0 4px 12px rgba(0,0,0,0.25), 0 1px 0 rgba(255,255,255,0.09) inset;
          font-size: 15px;
        }
        .btn-fn:hover { background: rgba(255,255,255,0.13); }
        .btn-fn.active { background: rgba(255,255,255,0.05); }

        .btn-eq {
          background: linear-gradient(135deg, #00d4b8 0%, #00a896 100%);
          color: #001a16;
          border: none;
          box-shadow: 0 6px 20px rgba(0,212,184,0.35), 0 1px 0 rgba(255,255,255,0.3) inset;
          font-size: 22px;
          font-weight: 500;
        }
        .btn-eq:hover { box-shadow: 0 8px 28px rgba(0,212,184,0.45); filter: brightness(1.05); }
        .btn-eq.active { box-shadow: 0 3px 10px rgba(0,212,184,0.25); }

        .btn-op-active {
          background: rgba(0,210,185,0.28) !important;
          border-color: rgba(0,210,185,0.5) !important;
          box-shadow: 0 0 0 2px rgba(0,210,185,0.3), 0 4px 14px rgba(0,210,185,0.1) !important;
        }

        .op-indicator {
          display: inline-flex;
          align-items: center;
          gap: 6px;
          font-size: 11px;
          color: rgba(0,212,184,0.5);
          letter-spacing: 0.1em;
          text-transform: uppercase;
          padding: 0 12px 8px;
          font-family: 'Outfit', sans-serif;
          font-weight: 300;
          min-height: 22px;
        }

        .op-dot {
          width: 5px; height: 5px;
          border-radius: 50%;
          background: #00d4b8;
          opacity: 0.6;
          animation: pulse 1.4s ease-in-out infinite;
        }

        @keyframes pulse {
          0%, 100% { opacity: 0.6; transform: scale(1); }
          50% { opacity: 1; transform: scale(1.3); }
        }

        @media (max-width: 400px) {
          .calc-shell { width: 100vw; border-radius: 0; min-height: 100vh; justify-content: center; display: flex; flex-direction: column; }
        }
      `}</style>

      <div className="calc-shell">
        {/* Display */}
        <div className="display-area">
          <div className="expression-text">{expression || "\u00a0"}</div>
          <div className={`display-text ${display === "ERR" ? "err" : ""}`}
            style={{ fontSize: displayLen > 10 ? "28px" : displayLen > 7 ? "38px" : "52px" }}>
            {display}
          </div>
        </div>

        {/* Active operator indicator */}
        <div className="op-indicator">
          {op && waitingForOperand ? <><div className="op-dot"/>{op}</> : "\u00a0"}
        </div>

        <div className="divider"/>

        {/* Buttons */}
        <div className="btn-grid">
          {BUTTONS.map(({ label, type }) => {
            const isActiveOp = type === "op" && op === label && waitingForOperand;
            const isActive = activeKey === label;
            const cls = [
              "btn",
              type === "num" ? "btn-num" :
              type === "op"  ? "btn-op"  :
              type === "eq"  ? "btn-eq"  : "btn-fn",
              isActive ? "active" : "",
              isActiveOp ? "btn-op-active" : "",
            ].join(" ");

            return (
              <button
                key={label}
                className={cls}
                onPointerDown={() => handleButton(label, type)}
                onContextMenu={(e) => e.preventDefault()}
              >
                {label}
              </button>
            );
          })}
        </div>
      </div>
    </div>
  );
}
