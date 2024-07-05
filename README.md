#Directory structure 
chat-app/
├── public/
│   └── index.html
├── src/
│   ├── App.js
│   ├── index.js
├── tests/
│   └── App.test.js
├── package.json
├── webpack.config.js
├── .babelrc
├── .gitignore
└── styles.css

#html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chat App</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div id="root"></div>
    <script src="../build/bundle.js"></script>
</body>
</html>

#javascript
import React, { useState } from 'react';
import './styles.css';

const App = () => {
    const [messages, setMessages] = useState([]);
    const [input, setInput] = useState('');

    const sendMessage = () => {
        setMessages([...messages, input]);
        setInput('');
    };

    return (
        <div className="chat-container">
            <div className="message-container">
                {messages.map((message, index) => (
                    <div key={index} className="message">{message}</div>
                ))}
            </div>
            <div className="input-container">
                <input 
                    type="text" 
                    value={input} 
                    onChange={(e) => setInput(e.target.value)} 
                    onKeyPress={(e) => e.key === 'Enter' && sendMessage()}
                    className="input-box"
                    placeholder="Type your message..."
                />
                <button onClick={sendMessage} className="send-button">Send</button>
            </div>
        </div>
    );
};

export default App;


#json
{
  "name": "chat-app",
  "version": "1.0.0",
  "main": "src/index.js",
  "scripts": {
    "start": "webpack serve --mode development",
    "build": "webpack --mode production",
    "test": "jest"
  },
  "dependencies": {
    "react": "^17.0.2",
    "react-dom": "^17.0.2"
  },
  "devDependencies": {
    "@babel/core": "^7.14.6",
    "@babel/preset-env": "^7.14.5",
    "@babel/preset-react": "^7.14.5",
    "babel-loader": "^8.2.2",
    "jest": "^27.0.6",
    "webpack": "^5.39.1",
    "webpack-cli": "^4.7.2",
    "webpack-dev-server": "^4.0.0"
  }
}

#webpack config
const path = require('path');

module.exports = {
    entry: './src/index.js',
    output: {
        path: path.resolve(__dirname, 'build'),
        filename: 'bundle.js',
        publicPath: '/build/'
    },
    module: {
        rules: [
            {
                test: /\.(js|jsx)$/,
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader'
                }
            },
            {
                test: /\.css$/,
                use: ['style-loader', 'css-loader']
            }
        ]
    },
    devServer: {
        contentBase: path.join(__dirname, 'public'),
        compress: true,
        port: 3000
    }
};


{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}

node_modules
build
.DS_Store

/* After I have reset some default styling */
body, html {
    margin: 0;
    padding: 0;
    height: 100%;
    width: 100%;
    font-family: Arial, sans-serif;
}

/* Basic styling for the chat container */
.chat-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100%;
    background-color: #f0f0f0;
    padding: 20px;
}

/* Styling for the message container */
.message-container {
    width: 100%;
    max-width: 600px;
    border: 1px solid #ccc;
    border-radius: 8px;
    overflow: hidden;
    margin-bottom: 20px;
    background-color: #fff;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
}

/* Styling for individual messages */
.message {
    padding: 10px;
    border-bottom: 1px solid #eee;
}

/* Input box and send button styling */
.input-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    max-width: 600px;
    margin-top: 10px;
}

.input-box {
    flex: 1;
    padding: 10px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

.send-button {
    background-color: #007bff;
    color: #fff;
    border: none;
    padding: 10px 20px;
    font-size: 16px;
    border-radius: 4px;
    cursor: pointer;
}

.send-button:hover {
    background-color: #0056b3;
}
