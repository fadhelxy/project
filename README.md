import React, { useState } from 'react';

export default function Kalkulator() {
  const [input, setInput] = useState('');
  const [result, setResult] = useState('');

  const handleClick = (value) => {
    setInput(input + value);
  };

  const handleClear = () => {
    setInput('');
    setResult('');
  };

  const handleBackspace = () => {
    setInput(input.slice(0, -1));
  };

  const handleEqual = () => {
    try {
      setResult(eval(input).toString()); // Catatan: `eval` bisa berbahaya, hanya untuk contoh!
    } catch {
      setResult('Error');
    }
  };

  return (
    <div className="max-w-sm mx-auto mt-10 p-4 bg-white rounded-2xl shadow-lg">
      <h1 className="text-2xl font-bold mb-4 text-center">Kalkulator</h1>
      <div className="mb-2 bg-gray-100 p-3 rounded text-right font-mono text-lg">
        <div>{input || '0'}</div>
        <div className="text-green-500">{result}</div>
      </div>
      <div className="grid grid-cols-4 gap-2">
        {['7','8','9','/', '4','5','6','*', '1','2','3','-', '0','.','=','+'].map((btn) => (
          <button
            key={btn}
            className="bg-blue-500 text-white p-3 rounded hover:bg-blue-600"
            onClick={() => btn === '=' ? handleEqual() : handleClick(btn)}
          >
            {btn}
          </button>
        ))}
        <button className="col-span-2 bg-red-500 text-white p-3 rounded hover:bg-red-600" onClick={handleClear}>C</button>
        <button className="col-span-2 bg-yellow-500 text-white p-3 rounded hover:bg-yellow-600" onClick={handleBackspace}>⌫</button>
      </div>
    </div>
  );
}
