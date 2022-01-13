<html>

<head>
    <meta http-equiv="Cache-Control" content="no-cache, no-store, must-revalidate" />
    <meta http-equiv="Pragma" content="no-cache" />
    <meta http-equiv="Expires" content="0" />
    <style>
        #result {
            background-color: grey;
        }
    </style>
</head>

<body>
    <h1>hellow world for login</h1><br/>


    <button onclick="statusCheck()">
       status check/reading token
    </button> <br /><br /><br />
    <button onclick="login()">
       Login
    </button> <br /><br /><br />

    <button onclick="query_report()">query report</button>
    <br/><br/>
    <div id='result'>result here</div>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>

    <script>

        accessToken = '0'
        rURL = ''
        window.fbAsyncInit = function () {
            FB.init({
                appId: '462910531970000',
                cookie: true,
                xfbml: true,
                version: 'v10.0'
            });

            FB.AppEvents.logPageView();

        };

        (function (d, s, id) {
            var js, fjs = d.getElementsByTagName(s)[0];
            if (d.getElementById(id)) { return; }
            js = d.createElement(s); js.id = id;
            js.src = "https://connect.facebook.net/en_US/sdk.js";
            fjs.parentNode.insertBefore(js, fjs);
        }(document, 'script', 'facebook-jssdk'));

        function query_report() {
            rURL = 'https://graph.facebook.com/v5.0/2290993290983213/adnetworkanalytics/?access_token=' + accessToken + '&metrics=[%27fb_ad_network_imp%27%2C%27fb_ad_network_click%27]&breakdowns=[%27platform%27,%20%27placement%27]&since=2020-11-03&until=2020-11-03'
            axios({
                method: 'get', //통신 방식
                url: rURL, //통신할 페이지
                data: {} //인자로 보낼 데이터
            })
                .then(response => {
                    // document.getElementById('boom').innerText = response.data.num;
                    console.log(response.data);
                    console.log('stringfy result' + JSON.stringify(response.data))
                    document.getElementById('result').innerText = JSON.stringify(response.data)
                })
                .catch(error => {
                    //document.getElementById('boom').innerText = 'error';
                    console.log(error);
                })

        }
        function statusCheck() {
            FB.getLoginStatus(function (response) {
                console.log(response);
                accessToken = response.authResponse.accessToken;
                console.log('token:' + accessToken);
            });

        }

        function login() {
            FB.login(function (response) {
                console.log(response);


            }, { scope: 'email, public_profile, read_audience_network_insights, read_insights' });

        }
    </script>


</body>

</html>
