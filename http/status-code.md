#### HTTP状态码

> 摘自 Yii2 框架 [\yii\web\Respons](https://www.yiiframework.com/doc/api/2.0/yii-web-response#$httpStatuses-detail) 类

* 1xx - 信息响应
  + 100 => 'Continue',这个临时响应表明，迄今为止的所有内容都是可行的，客户端应该继续请求，如果已经完成，则忽略它。
  + 101 => 'Switching Protocols',该代码是响应客户端的 Upgrade 标头发送的，并且指示服务器也正在切换的协议。
  + 102 => 'Processing',此代码表示服务器已收到并正在处理该请求，但没有响应可用。
  + 103 => 'Early Hints', 此状态代码主要用于与Link 链接头一起使用，以允许用户代理在服务器仍在准备响应时开始预加载资源。
  + 118 => 'Connection timed out',
  
* 2xx - 成功响应
  + 200 => 'OK',
  + 201 => 'Created',
  + 202 => 'Accepted',
  + 203 => 'Non-Authoritative',
  + 204 => 'No Content',
  + 205 => 'Reset Content',
  + 206 => 'Partial Content',
  + 207 => 'Multi-Status',
  + 208 => 'Already Reported',
  + 210 => 'Content Different',
  + 226 => 'IM Used',
  
* 3xx - 重定向
  + 300 => 'Multiple Choices',
  + 301 => 'Moved Permanently',
  + 302 => 'Found',
  + 303 => 'See Other',
  + 304 => 'Not Modified',
  + 305 => 'Use Proxy',
  + 306 => 'Reserved',
  + 307 => 'Temporary Redirect',
  + 308 => 'Permanent Redirect',
  + 310 => 'Too many Redirect',
  
* 4xx - 客户端响应
    + 400 => 'Bad Request',
    + 401 => 'Unauthorized',
    + 402 => 'Payment Required',
    + 403 => 'Forbidden',
    + 404 => 'Not Found',
    + 405 => 'Method Not Allowed',
    + 406 => 'Not Acceptable',
    + 407 => 'Proxy Authentication Required',
    + 408 => 'Request Time-out',
    + 409 => 'Conflict',
    + 410 => 'Gone',
    + 411 => 'Length Required',
    + 412 => 'Precondition Failed',
    + 413 => 'Request Entity Too Large',
    + 414 => 'Request-URI Too Long',
    + 415 => 'Unsupported Media Type',
    + 416 => 'Requested range unsatisfiable',
    + 417 => 'Expectation failed',
    + 418 => 'I\'m a teapot',
    + 421 => 'Misdirected Request',
    + 422 => 'Unprocessable entity',
    + 423 => 'Locked',
    + 424 => 'Method failure',
    + 425 => 'Unordered Collection',
    + 426 => 'Upgrade Required',
    + 428 => 'Precondition Required',
    + 429 => 'Too Many Requests',
    + 431 => 'Request Header Fields Too Large',
    + 449 => 'Retry With',
    + 450 => 'Blocked by Windows Parental Controls',
    + 451 => 'Unavailable For Legal Reasons',
* 5xx - 服务端响应
    + 500 => 'Internal Server Error',
    + 501 => 'Not Implemented',
    + 502 => 'Bad Gateway or Proxy Error',
    + 503 => 'Service Unavailable',
    + 504 => 'Gateway Time-out',
    + 505 => 'HTTP Version not supported',
    + 507 => 'Insufficient storage',
    + 508 => 'Loop Detected',
    + 509 => 'Bandwidth Limit Exceeded',
    + 510 => 'Not Extended',
    + 511 => 'Network Authentication Required',
