---
title: What is Deadlock and how to avoid it?
date: 2020-08-02 14:53:39
tags:
---

Deadlock is a scenario where a set of processes is blocked because each process has acquired a lock on a particular resource and is waiting for another resource locked by some other process.

Let me give you an example:
Suppose process1 is making a transaction from one account (R1) to another account (R2), and for that, it will try to acquire a lock on resource R1 and R2.
At the same time, process2 is trying to transfer funds from one account (R2) to another account (R1), and for that, it will try to acquire a lock on resource R2 and R1.
In this scenario, process1 will acquire the lock on resource R1, and process2 will acquire the lock on resource R2, and they will keep on waiting for each other to release the resource.

![image](https://miro.medium.com/max/892/1*EuJkMgQ9Ia497_U4C6dDfw.gif)

How to avoid Deadlock?
In order to avoid deadlock, you have to acquire a lock in the fixed order.
Let me explain by resolving the above deadlock.
If process1 gets the lock on resource R1 and then R2, at the same time, process2 also tries to get the lock on resources in the same order as process1, i.e. On resource R1 and then R2 instead of R2 and then R1.
![image](https://miro.medium.com/max/656/1*0msjuSAoaPu1VdyRZnBK9w.png)
In this case, process2 has to wait for process1 to finish the transaction.
Once process1 commits the transaction successfully, it will release the locks on the resources; therefore process 2 will get the required resources in order to complete the transaction successfully without getting into the deadlock.

### 针对第一种造成死锁的原因，嵌套多个synchronized同步
首先建一个Account类，包括账户ID，账户名称，账户余额。
```java
 
public class Account {
 
	private int id;
	private String accName;
	private double balance = 100;
 
	public Account(String name) {
		this.accName = name;
	}
	
	public Account(int id,String name) {
		this.id = id;
		this.accName = name;
	}
	
	public int compareTo(double money){
		if(balance > money){
			return 1;
		}else if(balance == money){
			return 0;
		}else{
			return -1;
		}
	}
	
	public void in(double money){
		balance += money;
		System.out.println(accName+"中的余额："+balance);
	}
	
	public void out(double money){
		balance -= money;
		System.out.println(accName+"中的余额："+balance);
	}
	
	/**
	 * @return the accName
	 */
	public String getAccName() {
		return accName;
	}
 
	/**
	 * @param accName the accName to set
	 */
	public void setAccName(String accName) {
		this.accName = accName;
	}
 
	/**
	 * @return the balance
	 */
	public double getBalance() {
		return balance;
	}
 
	/**
	 * @param balance the balance to set
	 */
	public void setBalance(double balance) {
		this.balance = balance;
	}
 
	/**
	 * @return the id
	 */
	public int getId() {
		return id;
	}
 
	/**
	 * @param id the id to set
	 */
	public void setId(int id) {
		this.id = id;
	}
		
}
```
实现转账的方法：
```java
	/**
	 * 造成死锁的示例：通过synchronized同步代码块
	 * @param A
	 * @param B
	 * @param money
	 * @throws Exception
	 */
	public static void transferMoney(Account A,Account B,double money) throws Exception{
		if(A.compareTo(money) < 0){
			throw new Exception("余额不足!");
		}
		synchronized(A){
			System.out.println(Thread.currentThread().getName()+"获得了"+ A.getAccName() +"的锁");
			Thread.sleep(2000);//模拟2个线程同时进行，等待获得B锁，这样就造成了死锁
			synchronized (B) {
				System.out.println("获得了"+ B.getAccName() +"的锁");
				A.out(money);
				B.in(money);
			}
		}
	}
```
测试方法
```java
	public static void main(String[] args) {
		final Account[] accounts = new Account[2];
		accounts[0] = new Account(1,"zhangsan");
		accounts[1] = new Account(2,"lisi");
		new Thread(new Runnable() {
			@Override
			public void run() {
				try {
					transferMoney(accounts[0], accounts[1], 10);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		}).start();
		new Thread(new Runnable() {
			@Override
			public void run() {
				try {
					transferMoney(accounts[1], accounts[0], 10);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		}).start();
		
	}
```
测试结果：
![image](https://img-blog.csdnimg.cn/20190321150047575.png)
问题的原因开头已经提到了，zhangsan账户向lis账户转账首先获取了zhangsan的对象锁，lis同时向zhangsan转账获得了lisi的对象锁，此时zhangsan无法获得zhangsan的对象锁，lisi无法获取到zhangsan的对象锁，从而导致死锁。那么问题原因知道了，如何解决呢？

通过hashcode给对象锁排序，使得每次获取锁的顺序是一致的。这里对象的hashcode一般情况下是不一样的，如果为了保险起见可以使用对象的唯一ID进行排序也是可以的。
```java
	/**方法一
	 * 解决死锁的方法：根据hashcode给锁排序，按照一个指定的顺序加锁
	 * @param A
	 * @param B
	 * @param money
	 * @throws Exception
	 */
	public static void solveDeadLock1(Account A,Account B,double money) throws Exception{
		if(A.compareTo(money) < 0){
			throw new Exception("余额不足!");
		}
		if(A.hashCode()<B.hashCode()){
			synchronized(A){
				System.out.println(Thread.currentThread().getName()+"获得了"+ A.getAccName() +"的锁");
				Thread.sleep(2000);//模拟2个线程同时进行，等待获得B锁，这样就造成了死锁
				synchronized (B) {
					System.out.println("获得了"+ B.getAccName() +"的锁");
					A.out(money);
					B.in(money);
				}
			}
		}else{
			synchronized(B){
				System.out.println(Thread.currentThread().getName()+"获得了"+ A.getAccName() +"的锁");
				Thread.sleep(2000);//等待获得B锁，这样就造成了死锁
				synchronized (A) {
					System.out.println("获得了"+ B.getAccName() +"的锁");
					A.out(money);
					B.in(money);
				}
			}
		}
		
	}
	
	/**方法二
	 * 解决死锁的方法：根据对象的唯一值进行排序
	 * @param A
	 * @param B
	 * @param money
	 * @throws Exception
	 */
	public static void solveDeadLock2(Account A,Account B,double money) throws Exception{
		if(A.compareTo(money) < 0){
			throw new Exception("余额不足!");
		}
		if(A.getId()<B.getId()){
			synchronized(A){
				System.out.println(Thread.currentThread().getName()+"获得了"+ A.getAccName() +"的锁");
				Thread.sleep(2000);//模拟2个线程同时进行，等待获得B锁，这样就造成了死锁
				synchronized (B) {
					System.out.println("获得了"+ B.getAccName() +"的锁");
					A.out(money);
					B.in(money);
				}
			}
		}else{
			synchronized(B){
				System.out.println(Thread.currentThread().getName()+"获得了"+ A.getAccName() +"的锁");
				Thread.sleep(2000);//等待获得B锁，这样就造成了死锁
				synchronized (A) {
					System.out.println("获得了"+ B.getAccName() +"的锁");
					A.out(money);
					B.in(money);
				}
			}
		}
		
	}
```
执行结果：
![image](https://img-blog.csdnimg.cn/20190321151333385.png)