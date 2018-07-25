# thinkphp5.1-aliyunsms
thinkphp5.1 阿里云 大于短信

将目录下的aliyun_dysms.php拷贝到config目录

示例代码：
<pre>    
/**
     * 阿里云 大于短信 发送接口
     * @param $mobile 手机号码
     * @param $signname 签名
     * @param $templatecode  短信模板ID
     * @param array $templateparam  短信模板 传入参数
     * @return \think\response\Json
     */
    public function sendsms($mobile,$signname,$templatecode,$templateparam=array()){
        $templateparam = array(
            "code" => rand(100000,999999)
        );
        $sendsms = new \mangdin\alidysms\sendSms();
        $msg = json_decode($sendsms->sendsms($mobile, $signname, $templatecode, $templateparam),true);
        if ($msg['Code'] == 'OK'){
            Session::set('smscode',$templateparam['code']);
            return json(['code'=>200,'icon'=>6,'msg'=>'发送成功']);
        }else{
            return json(['code'=>500,'icon'=>5,'msg'=>$msg['Message']]);
        }
    }
    </pre>

可以放到公共函数全局调用
