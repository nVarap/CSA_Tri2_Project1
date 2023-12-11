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

    .explanation {
        margin-top: 20px;
    }
</style>

<div class="container">
    <label for="list-size">Enter list size:</label>
    <input type="number" id="list-size" min="1" value="20">
    <button id="generate-list-btn">Generate List</button>
    <div class="array-container" id="array-container"></div>
    <div class="buttons">
        <button id="insertion-btn">Insertion Sort</button>
        <button id="bubble-btn">Bubble Sort</button>
        <button id="merge-btn">Merge Sort</button>
        <button id="reset-btn">Reset Bars</button>
    </div>
    <div class="explanation" id="explanation-container"></div>
</div>

<script>
    let delayTime = 200;
    let arrayContainer;
    let explanationContainer;
    let finalList;

    document.addEventListener('DOMContentLoaded', () => {
        // Initial setup
        arrayContainer = document.getElementById('array-container');
        explanationContainer = document.getElementById('explanation-container');
        setupListeners();
        generateBars();
    });

    function setupListeners() {
        document.getElementById('insertion-btn').addEventListener('click', () => insertionSort());
        document.getElementById('bubble-btn').addEventListener('click', () => bubbleSort());
        document.getElementById('merge-btn').addEventListener('click', () => mergeSort());
        document.getElementById('reset-btn').addEventListener('click', () => {
            generateBars();
            clearExplanation();
        });

        document.getElementById('generate-list-btn').addEventListener('click', () => generateList());
    }

    function generateList() {
        const listSize = parseInt(document.getElementById('list-size').value);
        // const generatedList = generateBars(listSize);
        console.log('Generated List:', generatedList);
        finalList = generatedList;
    }

    function generateBars(size = 20) {
        arrayContainer.innerHTML = '';

        const generatedList = [];

        for (let i = 0; i < size; i++) {
            const barHeight = Math.floor(Math.random() * 300) + 50; // Random height between 50 and 350
            const bar = document.createElement('div');
            bar.style.height = `${barHeight}px`;
            bar.classList.add('bar');
            arrayContainer.appendChild(bar);

            // Push the bar height to the generated list
            generatedList.push(barHeight);
        }

        return generatedList;
    }

    function delay(ms) {
        return new Promise(resolve => setTimeout(resolve, ms));
    }

    function clearExplanation() {
        explanationContainer.innerHTML = '';
    }

    async function insertionSort() {
        clearExplanation();
        explanationContainer.innerText = "Insertion Sort is a simple sorting algorithm that builds the final sorted array one element at a time. It iterates through the input data, comparing each element with the previous ones and swapping them until the entire sequence is ordered. This method is particularly efficient for small datasets but may become less practical for larger ones due to its quadratic time complexity. What you're seeing here is the swapping of each bigger bar until the array is sorted.";

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

            // Update visualization
            await updateVisualization(array);
        }
    }

    async function bubbleSort() {
        clearExplanation();
        explanationContainer.innerText = "Bubble Sort is another elementary sorting algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The pass through the list is repeated until the list is sorted. Though conceptually simple, its quadratic time complexity makes it less efficient for large datasets compared to more advanced algorithms. What you're seeing here is the swapping of a smaller bar with a bigger bar to change the out-of-order list to sort from least to greatest, one swap at a time.";

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
                    await updateVisualization(array);
                }
            }
        }
    }

async function mergeSort() {
    clearExplanation();
    explanationContainer.innerText = "Merge Sort, on the other hand, is a divide-and-conquer algorithm that recursively divides the input into smaller sections, sorts them individually, and then merges them back together. It achieves a stable, consistent performance with a time complexity of O(n log n), making it suitable for larger datasets. While its space complexity is higher due to the need for additional memory, Merge Sort's efficiency and predictability make it a popular choice for various applications, including external sorting. What you're seeing here is not a glitch. It's the list grouping and sorting itself by parts, combining each part with each other and sorting those until the whole list is sorted.";

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

        const leftResult = await mergeSortHelper(left);
        const rightResult = await mergeSortHelper(right);

        const mergedArray = await merge(leftResult, rightResult);

        // Update visualization after merging
        await updateVisualization(mergedArray);

        return mergedArray;
    }

    await mergeSortHelper(array);
    explanationContainer.innerText = "Merge Sort, on the other hand, is a divide-and-conquer algorithm that recursively divides the input into smaller sections, sorts them individually, and then merges them back together. It achieves a stable, consistent performance with a time complexity of O(n log n), making it suitable for larger datasets. While its space complexity is higher due to the need for additional memory, Merge Sort's efficiency and predictability make it a popular choice for various applications, including external sorting. What you're seeing here is not a glitch. It's the list grouping and sorting itself by parts, combining each part with each other and sorting those until the whole list is sorted.";
}

    async function updateVisualization(array) {
        arrayContainer.innerHTML = ''; // Clear the container

        // Append the bars directly to the existing arrayContainer
        array.forEach(bar => arrayContainer.appendChild(bar));

        // Add a delay
        await delay(delayTime);
    }
</script>
