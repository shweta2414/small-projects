#typing code 
import React, { useState, useEffect } from 'react';

const TypingEffect = ({ sentence }) => {
  const [currentText, setCurrentText] = useState('');
  const [currentIndex, setCurrentIndex] = useState(0);

  useEffect(() => {
    const intervalId = setInterval(() => {
      if (currentIndex < sentence.length) {
        setCurrentText((prevText) => prevText + sentence[currentIndex]);
        setCurrentIndex((prevIndex) => prevIndex + 1);
      } else {
        clearInterval(intervalId); // Stop interval after displaying all characters
      }
    }, 100); // Adjust interval timing (e.g., 100ms for each character)
    
    return () => {
      clearInterval(intervalId); // Cleanup on component unmount
    };
  }, [currentIndex, sentence]);

  return (
    <div>
      <p>{currentText}</p>
      {currentIndex === sentence.length && (
        <p style={{ fontWeight: 'bold' }}>{sentence}</p>
      )}
    </div>
  );
};

// Example usage:
const App = () => {
  const sentence = "Hello, World! This is a typing effect.";

  return (
    <div>
      <h1>Typing Effect</h1>
      <TypingEffect sentence={sentence} />
    </div>
  );
};

export default App;

