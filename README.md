nah sekarang, edit button instagram, linkedin dan email itu menjadi beranimasi seperti ini


<!DOCTYPE html>
<html>
<head>
    <title>Interactive Social Buttons - Asri Yohana Sirait</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body { 
            background: #0d1117; 
            display: flex; 
            justify-content: center; 
            align-items: center; 
            height: 100vh; 
            margin: 0; 
            font-family: 'Arial', sans-serif;
            overflow: hidden;
        }
        .container {
            position: relative;
            width: 100%;
            height: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 50px;
        }
        .button {
            position: relative;
            padding: 15px 30px;
            border-radius: 15px;
            color: white;
            text-decoration: none;
            font-weight: bold;
            font-size: 16px;
            transition: all 0.3s ease;
            cursor: pointer;
            display: inline-block;
            box-shadow: 0 4px 15px rgba(0,0,0,0.3);
            border: 2px solid rgba(255,255,255,0.2);
        }
        .button:hover {
            transform: scale(1.05);
            box-shadow: 0 6px 20px rgba(0,0,0,0.4);
        }
        .instagram { 
            background: linear-gradient(135deg, #E4405F, #C13584); 
        }
        .linkedin { 
            background: linear-gradient(135deg, #0077B5, #005885); 
        }
        .email { 
            background: linear-gradient(135deg, #D14836, #B23121); 
        }
        .title {
            position: absolute;
            top: 50px;
            width: 100%;
            text-align: center;
            color: white;
            font-size: 28px;
            font-weight: bold;
        }
        .instruction {
            position: absolute;
            bottom: 50px;
            width: 100%;
            text-align: center;
            color: #8b949e;
            font-size: 16px;
        }
    </style>
</head>
<body>
    <div class="title">🎯 Try to Click Me! 🎯</div>
    
    <div class="container">
        <a href="https://www.instagram.com/srtyohana/" 
           class="button instagram" 
           onmousemove="avoidCursor(this, event)"
           onmouseleave="resetPosition(this)"
           target="_blank">
           ◉ Instagram
        </a>
        
        <a href="https://www.linkedin.com/in/asri-yohana-sirait-138779276" 
           class="button linkedin" 
           onmousemove="avoidCursor(this, event)"
           onmouseleave="resetPosition(this)"
           target="_blank">
           ◎ LinkedIn
        </a>
        
        <a href="mailto:asrisirait11@gmail.com" 
           class="button email" 
           onmousemove="avoidCursor(this, event)"
           onmouseleave="resetPosition(this)">
           ◉ Email
        </a>
    </div>
    
    <div class="instruction">🕹️ Move your cursor close to the buttons and watch them run away!</div>

    <script>
        function avoidCursor(element, event) {
            const rect = element.getBoundingClientRect();
            const mouseX = event.clientX;
            const mouseY = event.clientY;
            
            const centerX = rect.left + rect.width / 2;
            const centerY = rect.top + rect.height / 2;
            
            const deltaX = mouseX - centerX;
            const deltaY = mouseY - centerY;
            
            const distance = Math.sqrt(deltaX * deltaX + deltaY * deltaY);
            
            if (distance < 100) {
                const angle = Math.atan2(deltaY, deltaX);
                const escapeDistance = 150;
                
                // Calculate new position (opposite direction from cursor)
                let newX = centerX - Math.cos(angle) * escapeDistance;
                let newY = centerY - Math.sin(angle) * escapeDistance;
                
                // Keep buttons within viewport bounds
                const maxX = window.innerWidth - rect.width;
                const maxY = window.innerHeight - rect.height;
                
                newX = Math.max(rect.width, Math.min(maxX, newX));
                newY = Math.max(rect.height, Math.min(maxY, newY));
                
                // Apply the transformation
                const translateX = newX - centerX;
                const translateY = newY - centerY;
                
                element.style.transform = `translate(${translateX}px, ${translateY}px) scale(1.1)`;
                element.style.zIndex = '1000';
            }
        }
        
        function resetPosition(element) {
            // Reset button position when cursor leaves
            setTimeout(() => {
                element.style.transform = 'translate(0px, 0px) scale(1)';
                element.style.zIndex = 'auto';
            }, 1000);
        }
    </script>
</body>
</html>
