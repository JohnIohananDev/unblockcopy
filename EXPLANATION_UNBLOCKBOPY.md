# Explicação do Bookmarklet "UnblockCopy"  

Este arquivo explica como funciona o bookmarklet que libera copiar/colar em sites que bloqueiam essas funções.  
This file explains how the bookmarklet works to unblock copy/paste on websites that try to prevent it.

## Como funciona | How it works

1. **Intercepta eventos de bloqueio**  
   O script pega eventos como copiar, colar, selecionar texto e clique com o botão direito e impede que o site os bloqueie.  
   The script intercepts events like copy, paste, text selection, and right-click and stops the site from blocking them.

2. **Remove travas do site**  
   Qualquer função que o site tenha definido para impedir copiar/colar é removida.  
   Any functions the site set to block copy/paste are removed.

3. **Permite seleção de texto via CSS**  
   O script aplica um estilo CSS para que qualquer texto possa ser selecionado.  
   The script applies a CSS style so that all text can be selected.

4. **Mostra uma notificação**  
   Uma pequena mensagem aparece no canto da tela dizendo que copiar/colar foi liberado.  
   A small notification appears in the corner of the screen indicating copy/paste is now allowed.

## Resumo | Summary
O bookmarklet basicamente reverte todas as proteções que tentam impedir copiar/colar e dá um feedback visual ao usuário.  
The bookmarklet basically reverses all protections that try to block copy/paste and gives a visual feedback to the user.

## Script original | Original script
O script completo está no arquivo do bookmarklet `allowCopy.js` ou no campo de URL do favorito.  
The full script is in the bookmarklet file `allowCopy.js` or in the bookmark URL field.
