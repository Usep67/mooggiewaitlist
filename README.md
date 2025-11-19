import React, { useState } from 'react';

// Mooggie Waitlist — NO EMAIL SUBMIT FIXED VERSION
// Fixes: unterminated string caused by truncated className ("border-gray-")
// - Full animated rabbit background
// - Wallet Connect button only
// - Clean, complete JSX and className strings

export default function MooggieWaitlist() {
  const [connected, setConnected] = useState(false);
  const [connecting, setConnecting] = useState(false);

  function handleWalletConnect() {
    setConnecting(true);
    setTimeout(() => {
      setConnected(true);
      setConnecting(false);
    }, 900);
  }

  function handleDisconnect() {
    setConnected(false);
  }

  return (
    <div className="min-h-screen relative overflow-hidden bg-gradient-to-b from-white to-gray-50">
      {/* Animated rabbit background */}
      <div
        aria-hidden
        className="absolute inset-0 pointer-events-none -z-10 flex items-center justify-center"
      >
        <svg
          className="w-full h-full object-cover"
          viewBox="0 0 1200 800"
          preserveAspectRatio="xMidYMid slice"
          xmlns="http://www.w3.org/2000/svg"
        >
          <defs>
            <linearGradient id="bgGrad" x1="0" x2="1">
              <stop offset="0%" stopColor="#FFECEC" />
              <stop offset="100%" stopColor="#FFF6F0" />
            </linearGradient>
            <filter id="softShadow" x="-20%" y="-20%" width="140%" height="140%">
              <feDropShadow dx="0" dy="14" stdDeviation="28" floodOpacity="0.08" />
            </filter>
          </defs>

          <rect width="100%" height="100%" fill="url(#bgGrad)" />

          {/* multiple animated rabbits */}
          {[0, 1, 2, 3, 4].map((i) => {
            const cx = 160 + i * 200;
            const cy = 200 + (i % 2 === 0 ? -20 : 30);
            const delay = i * 0.6;
            return (
              <g
                key={i}
                transform={`translate(${cx}, ${cy})`}
                style={{ transformOrigin: 'center' }}
              >
                <g
                  style={{
                    animation: `float 6s ease-in-out ${delay}s infinite`,
                    opacity: 0.92,
                    filter: 'url(#softShadow)',
                  }}
                >
                  <ellipse cx="0" cy="60" rx="110" ry="90" fill="#FFF" />
                  <circle cx="25" cy="-25" r="48" fill="#FFF" />
                  <g transform="translate(45,-88)">
                    <ellipse cx="0" cy="0" rx="20" ry="48" transform="rotate(-12)" fill="#FFF" />
                    <ellipse cx="-50" cy="-8" rx="20" ry="52" transform="rotate(6)" fill="#FFF" />
                  </g>
                  <g transform="translate(45,-88)" fill="#FAD6E0">
                    <ellipse cx="0" cy="0" rx="8" ry="28" transform="rotate(-12)" />
                    <ellipse cx="-50" cy="-8" rx="8" ry="30" transform="rotate(6)" />
                  </g>
                  <g transform="translate(8,-28)">
                    <ellipse cx="-6" cy="-2" rx="6" ry="8" fill="#2B2B2B" />
                    <ellipse cx="20" cy="-2" rx="6" ry="8" fill="#2B2B2B" />
                  </g>
                  <g transform="translate(8,-8)" fill="#FFD6E5" opacity="0.9">
                    <ellipse cx="-22" cy="8" rx="12" ry="8" />
                    <ellipse cx="36" cy="8" rx="12" ry="8" />
                  </g>
                  <path d="M12 2 C 18 8, 12 12, 6 10" stroke="#E38CA0" strokeWidth="3" fill="none" strokeLinecap="round" />
                  <path d="M-65 20 Q -30 18 -10 30" stroke="#F5F5F5" strokeWidth="10" strokeLinecap="round" fill="none" opacity="0.95" />
                  <g transform="translate(60,46) rotate(-18)">
                    <path d="M0 0 L36 -20 L12 28 Z" fill="#FF8A5C" />
                    <path d="M26 -22 L32 -36 L16 -30 Z" fill="#86C66C" />
                  </g>
                </g>
              </g>
            );
          })}

          <style>{`
            @keyframes float {
              0% { transform: translateY(0px) translateX(0px) rotate(0.0deg); }
              25% { transform: translateY(-18px) translateX(6px) rotate(-1.0deg); }
              50% { transform: translateY(0px) translateX(0px) rotate(0.0deg); }
              75% { transform: translateY(18px) translateX(-6px) rotate(1.0deg); }
              100% { transform: translateY(0px) translateX(0px) rotate(0.0deg); }
            }
          `}</style>
        </svg>
      </div>

      {/* Header */}
      <header className="relative z-10 py-8 px-6 sm:px-12">
        <div className="max-w-6xl mx-auto flex items-center justify-between">
          <div className="flex items-center gap-4">
            <div className="w-12 h-12 rounded-full bg-white/80 backdrop-blur flex items-center justify-center shadow-md">
              <span className="font-extrabold text-pink-500 text-lg">M</span>
            </div>
            <h1 className="text-2xl sm:text-3xl font-semibold tracking-tight text-gray-900">Mooggie Waitlist</h1>
          </div>

          <div className="flex items-center gap-3">
            {!connected ? (
              <button
                onClick={handleWalletConnect}
                className="inline-flex items-center gap-2 rounded-2xl px-4 py-2 bg-gradient-to-r from-pink-400 to-pink-300 text-white shadow hover:from-pink-500 active:scale-95 transition-transform"
                aria-pressed={connecting}
              >
                {connecting ? 'Connecting…' : 'Wallet Connect'}
              </button>
            ) : (
              <div className="flex items-center gap-2">
                <div className="px-3 py-2 rounded-full bg-white/80 border shadow-sm text-sm">0xAb…D34f</div>
                <button
                  onClick={handleDisconnect}
                  className="rounded-full px-3 py-2 bg-white/50 border border-gray-200 text-sm hover:bg-gray-100"
                >
                  Disconnect
                </button>
              </div>
            )}
          </div>
        </div>
      </header>

      {/* Center content – no email submit */}
      <main className="relative z-10 flex-1 flex items-center justify-center px-6 py-12">
        <div className="max-w-3xl w-full backdrop-blur-sm bg-white/60 border border-white/30 rounded-3xl p-10 shadow-2xl text-center">
          <h2 className="text-3xl sm:text-4xl font-extrabold text-gray-900 leading-tight">Welcome to Mooggie</h2>
          <p className="mt-3 text-gray-700 max-w-xl mx-auto">Playful wallets, cute vibes, early access coming soon. Connect your wallet to stay tuned.</p>

          <div className="mt-8 flex items-center justify-center">
            {!connected ? (
              <button
                onClick={handleWalletConnect}
                className="rounded-xl px-6 py-3 bg-pink-500 text-white font-semibold shadow hover:bg-pink-600 active:scale-95 transition-transform"
                aria-label="Connect wallet"
              >
                {connecting ? 'Connecting…' : 'Connect Wallet'}
              </button>
            ) : (
              <div className="flex flex-col items-center gap-3">
                <div className="px-4 py-2 rounded-full bg-white/80 border shadow-sm text-sm">0xAb…D34f</div>
                <button
                  onClick={handleDisconnect}
                  className="rounded-full px-4 py-2 bg-white/50 border border-gray-200 text-sm hover:bg-gray-100"
                >
                  Disconnect
                </button>
              </div>
            )}
          </div>
        </div>
      </main>

      <footer className="relative z-10 py-8 px-6 sm:px-12">
        <div className="max-w-6xl mx-auto text-center text-sm text-gray-600">
          © {new Date().getFullYear()} Mooggie — playful wallets for everyone
        </div>
      </footer>

      {/* Small accessibility helper for reduced-motion users */}
      <style>{`@media (prefers-reduced-motion: reduce) { svg * { animation: none !important; } }`}</style>
    </div>
  );
}
