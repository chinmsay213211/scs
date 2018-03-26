# scs
demo project for my scs idea


peer0.org2.buyer.com
------------------
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.buyer.com/users/Admin@org2.buyer.com/msp
CORE_PEER_ADDRESS=peer0.org2.buyer.com:7051
CORE_PEER_LOCALMSPID="Org2MSP"
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.logistic.com/peers/peer0.org2.logistic.com/tls/ca.crt

peer1.org2.buyer.com
------------------
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.buyer.com/users/Admin@org2.buyer.com/msp
CORE_PEER_ADDRESS=peer1.org2.buyer.com:7051
CORE_PEER_LOCALMSPID="Org2MSP"
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.logistic.com/peers/peer1.org2.logistic.com/tls/ca.crt


peer0.org3.logistic.com
------------------
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org3.logistic.com/users/Admin@org3.logistic.com/msp
CORE_PEER_ADDRESS=peer0.org3.logistic.com:7051
CORE_PEER_LOCALMSPID="Org3MSP"
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org3.logistic.com/peers/peer0.org3.logistic.com/tls/ca.crt

peer1.org3.logistic.com
------------------
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org3.logistic.com/users/Admin@org3.logistic.com/msp
CORE_PEER_ADDRESS=peer1.org3.logistic.com:7051
CORE_PEER_LOCALMSPID="Org3MSP"
CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org3.logistic.com/peers/peer1.org3.logistic.com/tls/ca.crt


Create channel
---------------

export CHANNEL_NAME=mychannel

peer channel create -o orderer.myorderer.com:7050 -c $CHANNEL_NAME -f ./channel-artifacts/channel.tx --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/myorderer.com/orderers/orderer.myorderer.com/msp/tlscacerts/tlsca.myorderer.com-cert.

JOIN CHANNEL
-------------

peer channel join -b mychannel.block

ORG2
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.buyer.com/users/Admin@org2.buyer.com/msp CORE_PEER_ADDRESS=peer0.org2.buyer.com:7051 CORE_PEER_LOCALMSPID="Org2MSP" CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.buyer.com/peers/peer0.org2.buyer.com/tls/ca.crt peer channel join -b mychannel.block
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.buyer.com/users/Admin@org2.buyer.com/msp CORE_PEER_ADDRESS=peer1.org2.buyer.com:7051 CORE_PEER_LOCALMSPID="Org2MSP" CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org2.buyer.com/peers/peer1.org2.buyer.com/tls/ca.crt peer channel join -b mychannel.block

ORG3
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org3.logistic.com/users/Admin@org3.logistic.com/msp CORE_PEER_ADDRESS=peer0.org3.logistic.com:7051 CORE_PEER_LOCALMSPID="Org3MSP" CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org3.logistic.com/peers/peer0.org3.logistic.com/tls/ca.crt peer channel join -b mychannel.block
CORE_PEER_MSPCONFIGPATH=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org3.logistic.com/users/Admin@org3.logistic.com/msp CORE_PEER_ADDRESS=peer1.org3.logistic.com:7051 CORE_PEER_LOCALMSPID="Org3MSP" CORE_PEER_TLS_ROOTCERT_FILE=/opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/peerOrganizations/org3.logistic.com/peers/peer1.org3.logistic.com/tls/ca.crt peer channel join -b mychannel.block


UPDATE ANCHOR PEER:

peer channel update -o orderer.myorderer.com:7050 -c $CHANNEL_NAME -f ./channel-artifacts/Org1MSPanchors.tx --tls --cafile /opt/gopath/src/github.com/hyperledger/fabric/peer/crypto/ordererOrganizations/myorderer.com/orderers/orderer.myorderer.com/msp/tlscacerts/tlsca.myorderer.com-cert.pem
