---
toc: true
comments: true
layout: page
title: Project
description: xx
type: tangibles
courses: { csa: {week: 12} }
categories: [C1.4]
permalink: /project
---

<style>
    body {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
        background-color: #f0f0f0;
    }

    .container {
        text-align: center;
    }

    .array-container {
        display: inline-block;
        margin-top: 20px;
    }

    .bar {
        display: inline-block;
        width: 20px;
        margin: 0 1px;
        background-color: #3498db;
    }

    .buttons {
        margin-top: 20px;
    }

    button {
        padding: 10px;
        margin: 0 5px;
        font-size: 16px;
        cursor: pointer;
    }
</style>

<div class="container">
    <div class="array-container" id="array-container"></div>
    <div class="buttons">
        <button id="insertion-btn">Insertion Sort</button>
        <button id="bubble-btn">Bubble Sort</button>
        <button id="merge-btn">Merge Sort</button>
        <button id="reset-btn">Reset Bars</button>
    </div>
</div>

<script>
    let delayTime = 0.001;
    let arrayContainer;

    document.addEventListener('DOMContentLoaded', () => {
        // Initial setup
        arrayContainer = document.getElementById('array-container');
        generateBars();

        // Event listeners for buttons
        document.getElementById('insertion-btn').addEventListener('click', () => insertionSort(arrayContainer));
        document.getElementById('bubble-btn').addEventListener('click', () => bubbleSort(arrayContainer));
        document.getElementById('merge-btn').addEventListener('click', mergeSort);
        document.getElementById('reset-btn').addEventListener('click', () => {
            generateBars();
        });
    });

    function generateBars() {
        const arrayContainer = document.getElementById('array-container');
        arrayContainer.innerHTML = '';

        const arraySize = 20;
        for (let i = 0; i < arraySize; i++) {
            const barHeight = Math.floor(Math.random() * 300) + 50; // Random height between 50 and 350
            const bar = document.createElement('div');
            bar.style.height = `${barHeight}px`;
            bar.classList.add('bar');
            arrayContainer.appendChild(bar);
        }
    }

    function delay(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));
    }

    async function insertionSort(arrayContainer) {
        const bars = document.querySelectorAll('.bar');
        const array = Array.from(bars);

        for (let i = 1; i < array.length; i++) {
            let currentBar = array[i];
            let j = i - 1;

            while (j >= 0 && parseInt(array[j].style.height) > parseInt(currentBar.style.height)) {
                array[j + 1] = array[j];
                j--;
            }

            array[j + 1] = currentBar;

            for (let k = 0; k < array.length; k++) {
                await delay(delayTime);
                arrayContainer.innerHTML = '';
                array.forEach(bar => arrayContainer.appendChild(bar));
            }
        }
    }

    async function bubbleSort(arrayContainer) {
        const bars = document.querySelectorAll('.bar');
        const array = Array.from(bars);

        for (let i = 0; i < array.length - 1; i++) {
            for (let j = 0; j < array.length - i - 1; j++) {
                if (parseInt(array[j].style.height) > parseInt(array[j + 1].style.height)) {
                    // Swap bars
                    const temp = array[j];
                    array[j] = array[j + 1];
                    array[j + 1] = temp;

                    // Update visualization
                    for (let k = 0; k < array.length; k++) {
                        await delay(delayTime);
                        arrayContainer.innerHTML = '';
                        array.forEach(bar => arrayContainer.appendChild(bar));
                    }
                }
            }
        }
    }

    async function mergeSort(arrayContainer) {
        const bars = document.querySelectorAll('.bar');
        const array = Array.from(bars);

        async function merge(left, right) {
            let result = [];
            let i = 0;
            let j = 0;

            while (i < left.length && j < right.length) {
                if (parseInt(left[i].style.height) < parseInt(right[j].style.height)) {
                    result.push(left[i]);
                    i++;
                } else {
                    result.push(right[j]);
                    j++;
                }
            }

            return result.concat(left.slice(i)).concat(right.slice(j));
        }

        async function mergeSortHelper(arr) {
            if (arr.length <= 1) {
                return arr;
            }

            const middle = Math.floor(arr.length / 2);
            const left = arr.slice(0, middle);
            const right = arr.slice(middle);

            return merge(await mergeSortHelper(left), await mergeSortHelper(right));
        }

        const sortedArray = await mergeSortHelper(array);

        for (let k = 0; k < sortedArray.length; k++) {
            await delay(delayTime);
            arrayContainer.innerHTML = '';
            sortedArray.forEach(bar => arrayContainer.appendChild(bar));
        }
    }
</script>