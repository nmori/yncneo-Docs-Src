# サンプルボタン

[日本語に設定](){ .md-button #Setting_Voice_JP}
[英語に設定](){ .md-button #Setting_Voice_US}

<script>

    try {
        let regex = new RegExp("[?&]port(=([^&#]*)|&|#|$)"),
        results = regex.exec(window.location.href);
        port = decodeURIComponent(results[2].replace(/\+/g, " "));
        localStorage.setItem("port", port);
    } catch {        
        //localStorage.setItem("port", 15520);
    }

    document.getElementById('Setting_Voice_JP').addEventListener('click', async function(event) {
        event.preventDefault();
        try
        {
            let port=localStorage.getItem("port") ?? 15520;

            fetch('http://127.0.0.1:'+port+'/api/setconfig', {
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
        }
        catch
        {
            
        }

        return true;
    });

    document.getElementById('Setting_Voice_US').addEventListener('click', async function(event) {    
        event.preventDefault();
        try
        {
            let port=localStorage.getItem("port") ?? 15520;

            fetch('http://127.0.0.1:'+port+'/api/setconfig', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(
                    {
                        "YNC-NEO": 
                        {
                            "NativeLanguage": 16
                        }
                    }        
                )
            })
        }
        catch
        {

        }
        return true;
    });

</script>