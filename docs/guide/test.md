# サンプルボタン

[日本語に設定](){ .md-button #postButton}

<script>
document.getElementById('postButton').addEventListener('click', function() {
    fetch('http://127.0.0.1:15520/api/setconfig', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(
            {
                "YNC-NEO": 
                {
                    "NativeLanguage": 43
                }
            }        
        )
    })
    .then(response => response.json())
    .then(data => console.log('成功:', data))
    .catch((error) => console.error('エラー:', error));
    return false;
});
</script>