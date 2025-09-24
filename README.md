# UnblockCopy (Bookmark)
A tiny bookmarklet that restores paste, selection and right‑click on pages that try to block them.
Um pequeno bookmarklet que reativa colar, seleção e menu de contexto em páginas que impõem bloqueios.

## Como usar | How to use:
Crie um favorito e cole o script abaixo no campo de URL; depois acione o favorito na página restrita.
Create a new bookmark and paste the script below into the URL field; then trigger the bookmark on the restricted page.

### Script
``` javascript:(function(){function remove_block(){const h=e=>{e.stopImmediatePropagation();return!0};["copy","cut","paste","contextmenu","selectstart","mousedown"].forEach(ev=>document.addEventListener(ev,h,!0));document.oncopy=document.oncut=document.onpaste=document.oncontextmenu=document.onselectstart=null;var s=document.createElement("style");s.textContent="*{user-select:text!important;-webkit-user-select:text!important;-moz-user-select:text!important;}";document.head.appendChild(s);var old=document.getElementById("__allowcopy_note");if(old)old.remove();var d=document.createElement("div");d.id="__allowcopy_note";d.textContent="✓ Copiar/colar liberado";Object.assign(d.style,{position:"fixed",top:"20px",right:"20px",padding:"12px 18px",background:"rgba(32,32,32,0.85)",color:"#fff",fontFamily:"system-ui,sans-serif",fontSize:"14px",borderRadius:"8px",boxShadow:"0 4px 20px rgba(0,0,0,0.25)",zIndex:2147483647,opacity:"0",transform:"translateY(-10px)",transition:"all .4s ease"});document.body.appendChild(d);requestAnimationFrame(()=>{d.style.opacity="1";d.style.transform="translateY(0)"});setTimeout(()=>{d.style.opacity="0";d.style.transform="translateY(-10px)"},2500);setTimeout(()=>{d.remove()},3000)}remove_block();})(); ```
