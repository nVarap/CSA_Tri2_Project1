---
comments: true
layout: post
title: SASS UI Demo
description: xx
type: tangibles
toc: true
courses: { csse: {week: 0}, csp: {week: 0}, csa: {week: 0} }
categories: [C4.1]
permalink: /sass-ui-demo
---

<style>
.card, .card-three, .card-two, .card-one {
  background-color: #ecf0f1;
  border-radius: 8px;
  padding: 20px;
  margin: 20px;
  width: 300px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s ease-in-out;
}
.card:hover, .card-three:hover, .card-two:hover, .card-one:hover {
  background-color: #bdc3c7;
}
.card h2, .card-three h2, .card-two h2, .card-one h2 {
  color: #3498db;
  margin-bottom: 10px;
}
.card p, .card-three p, .card-two p, .card-one p {
  color: #2ecc71;
}
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.card-three h2 {
  color: #e74c3c;
}
.card-three p {
  color: #f39c12;
}
</style>

<div class="container">
  <div class="card">
    <h2>Card One</h2>
    <p>This is the content of card one.</p>
  </div>

  <div class="card-two">
    <h2>Card Two</h2>
    <p>This is the content of card two.</p>
  </div>

  <div class="card-three">
    <h2>Card Three</h2>
    <p>This is the content of card three with custom colors.</p>
  </div>
</div>