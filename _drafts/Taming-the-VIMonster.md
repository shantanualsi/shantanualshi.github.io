---
id: 380
title: Taming the VIMonster
date: 2017-02-26T23:33:25+08:00
author: shantanualshi
layout: post
guid: https://shantanualshi.wordpress.com/?p=380
permalink: /?p=380
categories:
  - Uncategorized
---
<a href="https://shantanualshi.wordpress.com/2016/07/03/the-monster-known-as-vim/" target="_blank" rel="noopener noreferrer">My previous post</a> would have helped you get familiar with the logic behind VIM&#8217;s commands.  We covered the modes that VIM operates in, its Alphabet and some grammar viz. Imperatives and prepositions.

This post will introduce you to the extended alphabet and visual modes.

## Block Alphabet

Block letters in VIM are not that many. As usual alphabet works around with letters or words as the subject, block letters usually work with the entire line (with some exceptions). Go through some of these examples &#8211;

<div style="direction:ltr;">
  <table style="direction:ltr;border-collapse:collapse;border:1pt solid #A3A3A3;" title="" border="1" summary="" cellspacing="0" cellpadding="0">
    <tr>
      <td style="vertical-align:top;width:2.4486in;padding:4pt;border:1pt solid #A3A3A3;">
        <p style="margin:0;font-family:Calibri;font-size:11pt;">
          A: Append to the end of the line
        </p>
      </td>
      
      <td style="vertical-align:top;width:2.2097in;padding:4pt;border:1pt solid #A3A3A3;">
        <p style="margin:0;font-family:Calibri;font-size:11pt;">
          H: Start of the document in view
        </p>
      </td>
    </tr>
    
    <tr>
      <td style="vertical-align:top;width:2.4486in;padding:4pt;border:1pt solid #A3A3A3;">
        <p style="margin:0;font-family:Calibri;font-size:11pt;">
          C: Change the entire line
        </p>
      </td>
      
      <td style="vertical-align:top;width:2.1486in;padding:4pt;border:1pt solid #A3A3A3;">
        <p style="margin:0;font-family:Calibri;font-size:11pt;">
          O: Open line on the top
        </p>
      </td>
    </tr>
    
    <tr>
      <td style="vertical-align:top;width:2.4486in;padding:4pt;border:1pt solid #A3A3A3;">
        <p style="margin:0;font-family:Calibri;font-size:11pt;">
          D: Delete the entire line
        </p>
      </td>
      
      <td style="vertical-align:top;width:2.1486in;padding:4pt;border:1pt solid #A3A3A3;">
        <p style="margin:0;font-family:Calibri;font-size:11pt;">
          R: Replace until Esc is pressed
        </p>
      </td>
    </tr>
    
    <tr>
      <td style="vertical-align:top;width:2.4486in;padding:4pt;border:1pt solid #A3A3A3;">
        <p style="margin:0;font-family:Calibri;font-size:11pt;">
          G: End of the document
        </p>
      </td>
      
      <td style="vertical-align:top;width:2.1486in;padding:4pt;border:1pt solid #A3A3A3;">
        <p style="margin:0;font-family:Calibri;font-size:11pt;">
          S: Substitute entire line
        </p>
      </td>
    </tr>
    
    <tr>
      <td style="vertical-align:top;width:2.4486in;padding:4pt;border:1pt solid #A3A3A3;">
        <p style="margin:0;font-family:Calibri;font-size:11pt;">
          Q: Enter Ex mode
        </p>
      </td>
      
      <td style="vertical-align:top;width:2.1486in;padding:4pt;border:1pt solid #A3A3A3;">
        <p style="margin:0;font-family:Calibri;font-size:11pt;">
          L: End of the document in view
        </p>
      </td>
    </tr>
  </table>
</div>

&nbsp;

The Extended Alphabet

&nbsp;

cc &#8211; Cut the entire line

gg &#8211; Go to the start of the document

dd &#8211; Delete the entire line

? &#8211; find backwards

Visual Modes

Visual modes is a fancy name for selection. VIM allows you to select text just as you would in a usual text editor that too without using your mouse. The way to enter visual mode is to press &#8216;v&#8217;.

substitute in visual mode

Visual Block

Ctrl + V

Ctrl + P

&nbsp;

Ctrl + o &#8211; Where you came from backwards

Ctrl + i &#8211; Go forward where you came from

Write about multiple cursors, visual modes, search Regex and other regexs and commands like gg, GG etc.