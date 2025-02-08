---
title: GoodNote - 网页笔记助手 
date: 2025-02-08 00:00:00+0000
slug: goodnote-js
image: https://i.imgur.com/WBL8ZVa.png
---
[![Hits](https://hits.seeyoufarm.com/api/count/incr/badge.svg?url=https://b.kill9pid.top/p/goodnote-js/&count_bg=%23F26E00&title_bg=%23000000)](https://hits.seeyoufarm.com)

## GoodNote - 网页笔记助手
下载地址：
https://greasyfork.org/zh-CN/scripts/526070  

他是我最近一直在写的一个项目，功能是：可以在任何网页有一个小笔记，记录一些文本内容。

## 介绍：

📝 GoodNote - 网页笔记助手

✨ 自动分类：每个网站专属笔记空间，查找超便捷
🔒 安全可靠：笔记仅存本地，隐私有保障
💡 便捷操作：点击右上角按钮，随时记录
📌 即写即存：自动保存，不怕内容丢失
🎯 自由拖拽：按钮可拖动、贴边隐藏，不遮挡
🎈 快捷键：按下 ctrl+shift+M，快速呼出记录界面


✨ Auto - classification: Each website has its exclusive note space, making it extremely convenient for searching.
🔒 Secure and Reliable: Notes are stored only locally, ensuring privacy protection.
💡 Convenient Operation: Click the button in the upper - right corner to record at any time.
📌 Write - and - Save: Automatically saves to prevent content loss.
🎯 Free Dragging: The button can be dragged, tucked to the side and hidden without blocking the view.
🎈 Shortcut Key: Press "Ctrl + Shift + M" to quickly call up the recording interface.

## 使用的技术
主要都是 AI 帮我写 js ， 我也不是很懂....
能用就行! HAHAA

如果要我来分析的话我认为比较难写的是拖拽功能 , 还有自动贴边隐藏功能 .
更多的问题在于你需要去使用这个产品然后发现它的问题 , 发现一些可以改进的点和使用的痛点 , 然后再让 AI 帮你改 .


## source code

```
// ==UserScript==
// @name         GoodNote - 网页笔记助手
// @namespace    http://tampermonkey.net/
// @version      0.4a
// @description  在任何网页添加笔记功能
// @author       kasusa
// @license MIT
// @match        *://*/*
// @icon         https://www.google.com/s2/favicons?sz=64&domain=greasyfork.org
// @grant        GM_setValue
// @grant        GM_getValue
// @downloadURL https://update.greasyfork.org/scripts/526070/GoodNote%20-%20%E7%BD%91%E9%A1%B5%E7%AC%94%E8%AE%B0%E5%8A%A9%E6%89%8B.user.js
// @updateURL https://update.greasyfork.org/scripts/526070/GoodNote%20-%20%E7%BD%91%E9%A1%B5%E7%AC%94%E8%AE%B0%E5%8A%A9%E6%89%8B.meta.js
// ==/UserScript==

(function() {
    'use strict';

    // 创建样式
    const style = document.createElement('style');
    style.textContent = `

        .note-icon {
            /* 背景颜色 */
            backdrop-filter: blur(10px);
            background-color: #ffffff00;
            border: 1px solid #ffffff8f;
            /* 圆角 */
            border-radius: 10px;
            /* 固定位置 */
            position: fixed;
            /* 默认位置 */
            top: 20px;
            right: 20px;
            /* 大小 */
            width: 40px;
            height: 40px;
            cursor: move;
            z-index: 9999;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 2px 5px rgba(0,0,0,0.2);
            transition: 0.1s ease;
            user-select: none;
            will-change: transform;
            transform: translate3d(0, 0, 0);
            opacity: 1;
        }

        .note-icon:hover {
            transform: scale(1);
        }
        .note-icon:active {
            transform: scale(0.9);
        }

        .note-icon svg {
            width: 24px;
            height: 24px;
			fill: #409eff;
        }

        .note-container {
            border: 1px solid #fff;
            position: fixed;
            backdrop-filter: blur(10px);
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
            z-index: 9998;
            padding: 10px;
            transition: all 0.3s ease;
            opacity: 0;
            transform-origin: center;

        }

        .note-container.active {
            opacity: 1;
            transform: scale(1);
        }

        .note-textarea {
            background: #fff;
            color:#000;
            min-height: 250px;
            border: 1px solid #ddd;
            border-radius: 4px;
            padding: 12px;
            font-size: 14px;
            resize: all;
            font-family: Arial, sans-serif;
            line-height: 1.5;
            min-width: 350px;
        }

        .note-textarea:focus {
            outline: none;
        }

        .note-icon::after {
            content: 'Ctrl+Shift+M';
            position: absolute;
            background: rgba(0, 0, 0, 0.8);
            color: white;
            padding: 5px 8px;
            border-radius: 4px;
            font-size: 12px;
            white-space: nowrap;
            right: 100%;
            top: 50%;
            transform: translateY(-50%);
            margin-right: 10px;
            opacity: 0;
            transition: opacity 0.2s;
            pointer-events: none;
        }

        .note-icon:hover::after {
            opacity: 1;
        }
    `;
    document.head.appendChild(style);

    // 创建笔记图标
    const noteIcon = document.createElement('div');
    noteIcon.className = 'note-icon';

    // 根据平台设置不同的快捷键提示
    const isMac = /Mac|iPod|iPhone|iPad/.test(navigator.platform);
    noteIcon.setAttribute('data-shortcut', isMac ? '⌘+Shift+M' : 'Ctrl+Shift+M');

    // 修改样式内容，使用动态快捷键文本
    const shortcutText = isMac ? '⌘+Shift+M' : 'Ctrl+Shift+M';
    style.textContent = style.textContent.replace(
        '.note-icon::after { content: \'Ctrl+Shift+M\';',
        `.note-icon::after { content: '${shortcutText}';`
    );

    noteIcon.innerHTML = `
        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
            <path d="M14,10H19.5L14,4.5V10M5,3H15L21,9V19A2,2 0 0,1 19,21H5C3.89,21 3,20.1 3,19V5C3,3.89 3.89,3 5,3M5,12V14H19V12H5M5,16V18H14V16H5Z"/>
        </svg>
    `;

    // 创建笔记容器
    const noteContainer = document.createElement('div');
    noteContainer.className = 'note-container';

    // 创建文本框
    const textarea = document.createElement('textarea');
    textarea.className = 'note-textarea';
    textarea.placeholder = '在这里输入你的笔记...';

    noteContainer.appendChild(textarea);

    // 添加到页面
    document.body.appendChild(noteIcon);
    document.body.appendChild(noteContainer);

    // 获取当前域名作为存储键
    const storageKey = `goodnote_${window.location.hostname}`;
    const positionKey = `goodnote_position_${window.location.hostname}`;

    // 从localStorage加载笔记
    const savedNote = localStorage.getItem(storageKey);
    if (savedNote) {
        textarea.value = savedNote;
    }

    // 实现拖拽功能
    let isDragging = false;
    let currentX;
    let currentY;
    let initialX;
    let initialY;
    let xOffset = 0;
    let yOffset = 0;

    let rafId = null;

    noteIcon.addEventListener('mousedown', dragStart);
    document.addEventListener('mousemove', drag);
    document.addEventListener('mouseup', dragEnd);

    function dragStart(e) {
        if (e.target === noteIcon || noteIcon.contains(e.target)) {
            isDragging = true;
            const rect = noteIcon.getBoundingClientRect();
            initialX = e.clientX - rect.left;
            initialY = e.clientY - rect.top;
        }
    }

    function drag(e) {
        if (isDragging) {
            e.preventDefault();

            if (rafId) {
                cancelAnimationFrame(rafId);
            }

            rafId = requestAnimationFrame(() => {
                const newX = e.clientX - initialX;
                const newY = e.clientY - initialY;

                currentX = Math.min(Math.max(0, newX), window.innerWidth - noteIcon.offsetWidth);
                currentY = Math.min(Math.max(0, newY), window.innerHeight - noteIcon.offsetHeight);

                setTranslate(currentX, currentY);
            });
        }
    }

    function setTranslate(xPos, yPos) {
        const threshold = 20; // 贴边触发的阈值
        const iconWidth = noteIcon.offsetWidth;
        const iconHeight = noteIcon.offsetHeight;

        // 计算图标中心点到边缘的距离
        const distanceToLeft = xPos;
        const distanceToRight = window.innerWidth - (xPos + iconWidth);
        const distanceToTop = yPos;
        const distanceToBottom = window.innerHeight - (yPos + iconHeight);

        // 设置初始透明度
        noteIcon.style.opacity = '1';

        // 检查是否接近边缘
        if (distanceToLeft < threshold) {
            xPos = -iconWidth * 0.8;
        } else if (distanceToRight < threshold) {
            xPos = window.innerWidth - iconWidth * 0.2;
        }

        if (distanceToTop < threshold) {
            yPos = -iconHeight * 0.8;
        } else if (distanceToBottom < threshold) {
            yPos = window.innerHeight - iconHeight * 0.2;
        }

        noteIcon.style.left = `${xPos}px`;
        noteIcon.style.top = `${yPos}px`;
        noteIcon.style.right = 'auto';
        noteIcon.style.bottom = 'auto';
    }

    function dragEnd(e) {
        if (isDragging) {
            isDragging = false;

            // 使用 GM_setValue 保存全局位置
            GM_setValue('goodnote_global_position', {
                top: noteIcon.style.top,
                left: noteIcon.style.left
            });

            if (rafId) {
                cancelAnimationFrame(rafId);
            }
        }
    }

    // 修改加载保存位置的逻辑
    const savedPosition = GM_getValue('goodnote_global_position', null);
    if (savedPosition) {
        try {
            const { top, left } = savedPosition;
            setTranslate(parseInt(left), parseInt(top));
        } catch (e) {
            console.error('Failed to load saved position');
        }
    }

    // 修改笔记显示逻辑
    noteContainer.style.position = 'fixed';
    let isVisible = false;

    // 添加切换笔记显示的函数
    function toggleNote() {
        isVisible = !isVisible;

        if (isVisible) {
            // 每次显示笔记时重新从 localStorage 加载数据
            let savedNote = localStorage.getItem(storageKey);
            if (savedNote) {
                textarea.value = savedNote;
            }

            const iconRect = noteIcon.getBoundingClientRect();
            const windowWidth = window.innerWidth;
            const windowHeight = window.innerHeight;
            const noteHeight = 300;
            const padding = 10;

            let left = iconRect.right - padding;
            let top = Math.max(padding, iconRect.top);

            // 检查水平方向是否超出
            if (left + 400 > windowWidth) {
                left = iconRect.left - 360;
            }

            // 确保left不会小于padding
            left = Math.max(padding, left);

            // 确保容器完全在可视区域内
            if (top + noteHeight > windowHeight) {
                top = windowHeight - noteHeight - padding;
            }

            // 确保top不会小于padding
            top = Math.max(padding, top);

            noteContainer.style.top = `${top}px`;
            noteContainer.style.left = `${left}px`;
            noteContainer.style.display = 'block';

            requestAnimationFrame(() => {
                noteContainer.classList.add('active');
                // 添加一个短暂延时确保过渡动画开始后再聚焦
                setTimeout(() => {
                    textarea.focus();
                }, 50);
            });
        } else {
            noteContainer.classList.remove('active');
            setTimeout(() => {
                noteContainer.style.display = 'none';
            }, 300);
        }
    }

    // 添加快捷键监听
    document.addEventListener('keydown', (e) => {
        // 检查是否是 Mac
        const isMac = /Mac|iPod|iPhone|iPad/.test(navigator.platform);

        if ((isMac && e.metaKey || !isMac && e.ctrlKey) && e.shiftKey && e.key.toLowerCase() === 'm') {
            e.preventDefault(); // 阻止默认行为
            toggleNote();
        }
    });

    noteIcon.addEventListener('click', (e) => {
        if (!isDragging) {
            toggleNote();
        }
    });

    // 修改点击其他地方关闭笔记的逻辑
    document.addEventListener('click', (e) => {
        if (!noteContainer.contains(e.target) && !noteIcon.contains(e.target) && isVisible) {
            isVisible = false;
            noteContainer.classList.remove('active');
            setTimeout(() => {
                noteContainer.style.display = 'none';
            }, 300);
        }
    });

    // 自动保存功能
    let saveTimeout;
    textarea.addEventListener('input', () => {
        clearTimeout(saveTimeout);
        saveTimeout = setTimeout(() => {
            localStorage.setItem(storageKey, textarea.value);
        }, 500); // 延迟500ms保存，避免频繁保存
    });

    // 添加鼠标悬停时显示图标
    noteIcon.addEventListener('mouseenter', () => {
        const currentLeft = parseInt(noteIcon.style.left);
        const currentTop = parseInt(noteIcon.style.top);

        if (currentLeft < 0) {
            noteIcon.style.left = '0px';
        } else if (currentLeft > window.innerWidth - noteIcon.offsetWidth) {
            noteIcon.style.left = (window.innerWidth - noteIcon.offsetWidth) + 'px';
        }

        if (currentTop < 0) {
            noteIcon.style.top = '0px';
        } else if (currentTop > window.innerHeight - noteIcon.offsetHeight) {
            noteIcon.style.top = (window.innerHeight - noteIcon.offsetHeight) + 'px';
        }

        noteIcon.style.opacity = '1';
    });

    // 添加鼠标离开时隐藏图标
    noteIcon.addEventListener('mouseleave', () => {
        if (!isDragging) {
            const currentLeft = parseInt(noteIcon.style.left);
            const currentTop = parseInt(noteIcon.style.top);
            const threshold = 20;

            if (currentLeft <= threshold ||
                currentLeft >= window.innerWidth - noteIcon.offsetWidth - threshold ||
                currentTop <= threshold ||
                currentTop >= window.innerHeight - noteIcon.offsetHeight - threshold) {
                setTranslate(currentLeft, currentTop);
            }
        }
    });

    // 在页面加载时重置状态
    window.addEventListener('load', () => {
        GM_setValue('goodNoteIconInserted', false);
    });
})();


```
