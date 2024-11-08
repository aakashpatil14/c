// SPDX-License-Identifier:UNLICENSED

pragma solidity ^0.8.0;

contract bank{
    address public accholder;
    uint balance =0;
    constructor(){
        accholder=msg.sender;
    }
    
    function withdraw() payable public {
        require(balance>0,"you dont have enogh balance.");
        require(msg.sender==accholder,"you are not account owener");
        payable(msg.sender).transfer(balance);
        balance=balance-msg.value;
    }
    function deposite() public payable{
        require(msg.value>0,"you dont have enogh balance.");
        require(msg.sender==accholder,"you are not account holder");
        balance+=msg.value;
    }
    function showbalance() public view returns(uint){
        
        require(msg.sender==accholder,"you are not account holder");
        return balance;
    }
}//// SPDX-License-Identifier:UNLICENSED

pragma solidity ^0.8.0;

contract studentData{

    struct student{
        string name;
        uint256 rollno;
    }

    student[] public studentarr;

    function addstudent(string memory name,uint rollno) public {
        for(uint i=0;i<studentarr.length;i++){
            if(studentarr[i].rollno==rollno){
                revert("Student with this roll no is already exist");
            }
        }
        studentarr.push(student(name,rollno));
    }

    function getStudentLength() public view returns(uint){
        return studentarr.length;
    }
    function displayAllstudent() public view returns(student[] memory){
        return studentarr;
    }

    function getstudentbyindex(uint idx) public view returns(student memory){
        require(idx<studentarr.length,"index out of bound");
        return studentarr[idx];
    }
    fallback() external payable 
    {

    }
    receive() external payable { 
        
    }
}
