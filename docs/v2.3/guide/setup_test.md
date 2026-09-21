# サンプルボタン

<!-- version-banner -->
!!! warning "これは v2.3 向けのドキュメントです"
    内容は v2.3 時点で凍結しており、重大な誤りを除いて更新しません。最新版をお使いの方は [v3.0 版のこのページ](../../v3.0/guide/setup_test.md) をご覧ください。


[日本語に設定](){ .md-button #Setting_Voice_JP}
[英語に設定](){ .md-button #Setting_Voice_US}

<script>

    try {
        let regex = new RegExp("[?&]port(=([^&#]*)|&|#|$)"),
        results = regex.exec(window.location.href);
        port = decodeURIComponent(results[2].replace(/\+/g, " "));
        localStorage.setItem("port", port);
    } catch {        
        //localStorage.setItem("port", 11900);
    }

    document.getElementById('Setting_Voice_JP').addEventListener('click', async function(event) {
        event.preventDefault();
        try
        {
            let port=localStorage.getItem("port") ?? 11900;

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
            let port=localStorage.getItem("port") ?? 11900;

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