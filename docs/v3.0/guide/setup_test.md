# サンプルボタン

<!-- version-banner -->
!!! info ""
    ゆかコネNEO **v3.0** のドキュメントです。v2.3 をお使いの方は [v2.3 版のこのページ](../../v2.3/guide/setup_test.md) を、違いを知りたい方は [v2.3 から v3.0 への移行](../../mig/mig_neo_v3.0.md) をご覧ください。


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