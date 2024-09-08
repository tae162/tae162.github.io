---
title: "TG stock valuation"
layout: single
permalink: /get_kor_stock_one_value/
---

<div id="get_kor_stock_one_value">
  <input type="text" id="inputValue" placeholder="종목명">
  <button onclick="executePythonCode()">Valuation</button>
  <pre id="output"></pre>
</div>

<script>
function executePythonCode() {
    const inputValue = document.getElementById('inputValue').value;
    fetch(`https://api.github.com/repos/tae162/tg_stock/actions/workflows/tg_stock_kor_one_value.yml/dispatches`, {

        method: 'POST',
        headers: {
            'Authorization': `token YOUR_GITHUB_TOKEN`,
            'Accept': 'application/vnd.github.v3+json'
        },
        body: JSON.stringify({
            ref: 'main',
            inputs: {
                args: inputValue
            }
        })
    }).then(response => {
        if (response.ok) {
            document.getElementById('output').innerText = '코드가 실행되었습니다. 결과를 기다리세요.';
        } else {
            document.getElementById('output').innerText = '실행 오류가 발생했습니다.';
        }
    });
}
</script>