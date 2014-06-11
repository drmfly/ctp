ctp
===
ctp ineterface of golang (for linux64)
http://www.citicsf.com/download/ctp/


=================preparing=====================

install go
install swig


=================build package=================

export GOROOT=<your go root path>
cd ./src
./make.sh


=================how to use=================
package main

import (
	"ctp"
	"fmt"
)

var (
	front string = "tcp://asp-sim2-front1.financial-trading-platform.com:26205"
	api   ctp.CThostFtdcTraderApi
)

type TradeApi struct {
	ctp.ThostFtdcTraderSpiImplBase
}

//callback from c++ libararys
func (g *TradeApi) OnFrontConnected() {
	fmt.Printf("connected\n")
}

func main() {
	api = ctp.CThostFtdcTraderApiCreateFtdcTraderApi()
	api.RegisterSpi(ctp.GTrader(&TradeApi{}))
	api.RegisterFront(front)
	api.Init()
	api.Join()
}


=================more=================

i need a public account to test...





