# -<?php
define('API_KEY','توکن);
function makereq($method,$datas=[]){
    $url = "https://api.telegram.org/bot".API_KEY."/".$method;
    $ch = curl_init();
    curl_setopt($ch,CURLOPT_URL,$url);
    curl_setopt($ch,CURLOPT_RETURNTRANSFER,true);
    curl_setopt($ch,CURLOPT_POSTFIELDS,http_build_query($datas));
    $res = curl_exec($ch);
    if(curl_error($ch)){
        var_dump(curl_error($ch));
    }else{
        return json_decode($res);
    }
}
$update = json_decode(file_get_contents('php://input'));
var_dump($update);
$textmessage = isset($update->message->text)?$update->message->text:'';


if ($textmessage == '/start')
{
	$arz = file_get_contents("http://provps.ir/api/nerkh/index.php");
var_dump(makereq('sendMessage',[
        'chat_id'=>$update->message->chat->id,
        'text'=>$arz,
	'parse_mode'=>'Html',
    ]));
}
?>
