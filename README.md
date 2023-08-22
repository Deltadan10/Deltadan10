- 👋 Hi, I’m @Deltadan10
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
Deltadan10/Deltadan10 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract MiToken {
    string public nombre = "Mi Token";
    string public símbolo = "MT";
    uint8 public decimales = 18;
    uint256 public totalSupply = 1000000 * 10 ** uint256(decimales);
    
    mapping(address => uint256) public balanceOf;
    mapping(address => mapping(address => uint256)) public allowance;
    
    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);
    
    constructor() {
        balanceOf[msg.sender] = totalSupply;
    }
    
    function transfer(address to, uint256 value) public returns (bool success) {
        require(to != address(0), "Dirección inválida");
        require(balanceOf[msg.sender] >= value, "Saldo insuficiente");
        
        balanceOf[msg.sender] -= value;
        balanceOf[to] += value;
        emit Transfer(msg.sender, to, value);
        return true;
    }
    
    function approve(address spender, uint256 value) public returns (bool success) {
        allowance[msg.sender][spender] = value;
        emit Approval(msg.sender, spender, value);
        return true;
    }
    
    function transferFrom(address from, address to, uint256 value) public returns (bool success) {
        require(from != address(0), "Dirección inválida");
        require(to != address(0), "Dirección inválida");
        require(balanceOf[from] >= value, "Saldo insuficiente");
        require(allowance[from][msg.sender] >= value, "Asignación insuficiente");
        
        balanceOf[from] -= value;
        balanceOf[to] += value;
        allowance[from][msg.sender] -= value;
        emit Transfer(from, to, value);
        return true;
    }
}

