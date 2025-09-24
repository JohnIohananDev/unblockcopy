# Explicação do Bookmarklet "UnblockCopy"  
Explanation of the "UnblockCopy" Bookmarklet  

Este arquivo explica como funciona o bookmarklet que libera copiar/colar em sites que bloqueiam essas funções.  
This file explains how the bookmarklet works to unblock copy/paste on websites that try to prevent it.  

O código original está no arquivo `bookmark.js`.  
The original code is in the file `bookmark.js`.

---

## Como funciona | How it works

1. **Intercepta eventos de bloqueio / Intercepts blocking events**  
   O script pega eventos como copiar, colar, selecionar texto e clique com o botão direito e impede que o site os bloqueie.  
   The script intercepts events like copy, paste, text selection, and right-click and stops the site from blocking them.

2. **Remove travas do site / Removes site locks**  
   Qualquer função que o site tenha definido para impedir copiar/colar é removida.  
   Any functions the site set to block copy/paste are removed.

3. **Permite seleção de texto via CSS / Allows text selection via CSS**  
   O script aplica um estilo CSS para que qualquer texto possa ser selecionado.  
   The script applies a CSS style so that all text can be selected.

4. **Mostra uma notificação / Shows a notification**  
   Uma pequena mensagem aparece no canto da tela dizendo que copiar/colar foi liberado.  
   A small notification appears in the corner of the screen indicating copy/paste is now allowed.

---

## Código comentado | Commented code

```javascript
javascript:(function() {
    // Função principal que vai liberar copiar/colar
    // Main function that will unblock copy/paste
    function remove_block() {
        // Função que bloqueia o bloqueio de eventos do site
        // Function that stops the site's event blocking
        const h = e => {
            e.stopImmediatePropagation(); // impede que o evento original seja executado / prevents the original event from executing
            return !0; // retorna true / returns true
        };

        // Lista de eventos que geralmente os sites bloqueiam
        // List of events that websites usually block
        ["copy", "cut", "paste", "contextmenu", "selectstart", "mousedown"]
        .forEach(ev => document.addEventListener(ev, h, !0)); // adiciona nossa função para todos eles / add our function to all of them

        // Remove qualquer função que o site tenha colocado para bloquear copiar/colar
        // Remove any functions the site set to block copy/paste
        document.oncopy = document.oncut = document.onpaste = 
        document.oncontextmenu = document.onselectstart = null;

        // Cria um estilo CSS que permite selecionar qualquer texto
        // Create a CSS style to allow selecting any text
        var s = document.createElement("style");
        s.textContent = "*{user-select:text!important;-webkit-user-select:text!important;-moz-user-select:text!important;}";
        document.head.appendChild(s);

        // Remove aviso antigo se já existir
        // Remove old notification if it already exists
        var old = document.getElementById("__allowcopy_note");
        if(old) old.remove();

        // Cria uma notificação na tela avisando que copiar/colar foi liberado
        // Create a screen notification saying copy/paste is now allowed
        var d = document.createElement("div");
        d.id = "__allowcopy_note";
        d.textContent = "✓ Copiar/colar liberado / Copy/paste allowed";

        // Estilo da notificação (posição, cor, fonte, animação)
        // Notification style (position, color, font, animation)
        Object.assign(d.style, {
            position: "fixed",
            top: "20px",
            right: "20px",
            padding: "12px 18px",
            background: "rgba(32,32,32,0.85)",
            color: "#fff",
            fontFamily: "system-ui,sans-serif",
            fontSize: "14px",
            borderRadius: "8px",
            boxShadow: "0 4px 20px rgba(0,0,0,0.25)",
            zIndex: 2147483647,
            opacity: "0",
            transform: "translateY(-10px)",
            transition: "all .4s ease"
        });

        document.body.appendChild(d); // adiciona a notificação ao body / add the notification to the body

        // Faz a animação de aparecer
        // Animate notification to appear
        requestAnimationFrame(() => {
            d.style.opacity = "1";
            d.style.transform = "translateY(0)";
        });

        // Depois de 2,5 segundos, começa a sumir
        // After 2.5 seconds, start fading out
        setTimeout(() => {
            d.style.opacity = "0";
            d.style.transform = "translateY(-10px)";
        }, 2500);

        // Remove a notificação completamente após 3 segundos
        // Completely remove notification after 3 seconds
        setTimeout(() => { d.remove() }, 3000);
    }

    // Chama a função para liberar copiar/colar imediatamente
    // Call the function to unblock copy/paste immediately
    remove_block();
})();
