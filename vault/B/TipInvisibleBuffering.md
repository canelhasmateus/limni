# OnInvisibleBuffering


using [[ToolHAproxy]] is easy, but it silently introduces a new [[ProtocolTCP]] buffer.

The [[Cache]] spits out payload as quickly as possible, and the server sends data frames with the highest [[StreamWeight]] first.

The [[LoadBalancer]] foils this, since, as long as its tcp buffer is not completely filled, the lb will accept more data from the server: This quickly drains the server buffer, but from there on out, the priorization does not work anymore.

        HOL blocking
            Http2 solves the http head of line problem, it still suffers from tcp hol blocking : 
                tcp buffers are serialized fifos. this means that , once something is in that queue , you need to download it before going to the next one
                    .. Shouldn't multiplex solve this? 
    


    https://calendar.perfplanet.com/2018/http2-hol-waterfall/
