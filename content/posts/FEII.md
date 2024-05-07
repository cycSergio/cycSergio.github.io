---
title: FEII
subtitle:
date: 2023-10-31T10:57:45+08:00
draft: true
author:
  name:
  link:
  email:
  avatar:
description:
keywords:
license:
comment: false
weight: 0
tags:
  - draft
categories:
  - draft
hiddenFromHomePage: false
hiddenFromSearch: false
summary:
resources:
  - name: featured-image
    src: featured-image.jpg
  - name: featured-image-preview
    src: featured-image-preview.jpg
toc: true
math: false
lightgallery: false
password:
message:
repost:
  enable: true
  url:

# See details front matter: https://fixit.lruihao.cn/documentation/content-management/introduction/#front-matter
---

<!--more-->

# 顺丰一面 23/06/05

## HTML / CSS 

#### 盒模型

#### 行级元素和块级元素的区别

## JS 

#### this

#### call, apply, bind的区别

#### 原型和原型链

#### 闭包

## React 

## 网络相关

#### tcp协议几次挥手的过程



#### https为什么能保障安全，怎么做到加密的？



#### 在浏览器地址栏输入url到打开页面的过程中发生了什么？



## 算法

#### 说出3种排序方法及实现

##### Selection Sort  

- Works by finding the minimum of the unsorted and swapping it with the item at the current position (which is the end of the sorted)
- O(n^2) time on average and worst case
- O(1) space

```java
    /**
     * @param arr
     *
     * Sort the array arr in place using selection sort.
     * The selection sort algorithm is as follows:
     * 1. Find the minimum element in the array.
     * 2. Swap the minimum element with the first element in the array.
     * 3. Repeat steps 1 and 2, but ignoring the first element in the array.
     *
     * This should be an in-place sort, so you shouldn't create any additional arrays.
     */
    public static void sort(int[] arr) {
        // TODO: Implement selection sort
        int size = arr.length;
        int curMinIdx = 0;
        for (int i = 0; i < size; i++) {
            curMinIdx = min(arr, i);
            swap(arr, curMinIdx, i);
        }
    }
```

##### Insertion Sort 

- for each element, keep swapping it to the left until it's bigger than the left element. By doing this, we are building sorted sublist on the left side of the original list.
- O(n^2) time on average and worst case (the input list is reversed sorted) ; O(N) time on best case (the input list is already sorted)
- O(1) space
- Why use? : 1. very fast on small inputs (N < 15); 2. very fast when input list is heavily sorted

```java
    /**
     * @param arr
     *
     * Sort the array arr in place using insertion sort.
     * The insertion sort algorithm is as follows:
     * 1. Loop through each element in the array.
     * 2. While the element is smaller than the previous element in the array,
     *   swap the element with the previous element.
     *
     * This should be an in-place sort, so you shouldn't create any additional arrays.
     */
    public static void sort(int[] arr) {
        // TODO: Implement insertion sort
        int size = arr.length;
        for (int i = 1; i < size; i++) {
            while (arr[i] < arr[i - 1]) {
                swap(arr, i, i - 1);
                i -= 1;
                if (i < 1) {
                    break;
                }
            }
        }
    }
```

##### Merge Sort 

- Works by continually dividing the list in half until only two sublists of one item remain. Then we merge (and compare) items in each sublist until we have sorted the entire list. This also uses a divide and conquer approach.
- O(n log n) time on average, and O(n log n) in worst case
- O(n) space - used in the merge step

```java
    /* Returns a copy of this DLList sorted using merge sort. Does not modify
       the original DLList. */
    public DLList<T> mergeSort() {
        if (size <= 1) {
            return this;
        }
        DLList<T> oneHalf = new DLList<>();
        DLList<T> otherHalf = new DLList<>();
        // TODO: YOUR CODE HERE
        Node p = sentinel.next;
        //System.out.println(p.item);
        for (int i = 0; i < size; i++) {
            if (i < size/2) {
                oneHalf.addLast(p.item);
            } else {
                otherHalf.addLast(p.item);
            }
            p = p.next;
        }
        DLList<T> sortedOneHalf = oneHalf.mergeSort();
        DLList<T> sortedOtherHalf = otherHalf.mergeSort();
        return sortedOneHalf.merge(sortedOtherHalf);
    }
```



##### Quick  Sort

- Works by picking a value from the array to be a "pivot". Optimally this is chosen at random and swapped with the last item for convenience. We then partition the list
  such that the pivot is in the middle and all values less than the pivot are to its left and all values greater than the pivot are to its right. This is done recursively (until we only have one element left) using a divide and conquer approach
- O(n log n) time on average and O(n^2) in worst case
- O(n) space in worst case, O(1) if sorting the list in-place

```java
    /* Returns a copy of this DLList sorted using quicksort. The first element
       is used as the pivot. Does not modify the original DLList. */
    public DLList<T> quicksort() {
        if (size <= 1) {
            return this;
        }
        // Assume first element is the divider.
        DLList<T> smallElements = new DLList<>();
        DLList<T> largeElements = new DLList<>();
        T pivot = sentinel.next.item;

        DLList<T> equalElements = new DLList<>();
        Node p = sentinel.next;
        while (p != sentinel) {
            int cmp = p.item.compareTo(pivot);
            if (cmp < 0) {
                smallElements.addLast(p.item);
            } else if (cmp == 0) {
                equalElements.addLast(p.item);
            } else {
                largeElements.addLast(p.item);
            }
            p = p.next;
        }
        DLList<T> SortedSmallElements = smallElements.quicksort();
        DLList<T> SortedLargeElements =  largeElements.quicksort();
        SortedSmallElements.append(equalElements);
        SortedSmallElements.append(SortedLargeElements);
        return SortedSmallElements;
    }
```



# 北大信研院 1102

## 面试准备1101

算法只做做常见的，20道左右；想想怎么介绍自己的经历和项目；剩下全背八股

## Alg.

#### 二分查找

```java
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length  - 1;
        while (left <= right) {
            int mid = (left + right) / 2; 
            if (nums[mid] < target) {
                left = mid + 1;
            } else if (nums[mid] > target) {
                right = mid - 1;
            } else if (nums[mid] == target) {
                return mid;
            }
        }
        return -1;
    }
}
```

#### 排序

#### 二叉树

#### 斐波那契数列

```java
class Solution {
    public int fib(int n) {
        if (n <= 1) {
            return n;
        }
        int prev = 0, curr =1, temp;
        while (n > 0) {
            temp = prev + curr;
            prev = curr;
            curr = temp;
            n -= 1;
        }
        return prev;
    }
}

// 递归的话
class Solution {
    public int fib(int n) {
        if (n <= 1) {
            return n;
        }
        return fib(n - 1) + fib(n - 2);

    }
}
```

#### 字符串最长不重复子串 

代码中使用了滑动窗口的思想来解决这个问题。具体解释如下：

1. 声明一个 `Set` 类型的变量 `checked`，用于存储当前窗口中出现过的字符。
2. 初始化变量 `len` 为字符串 `s` 的长度，`right` 为 -1，表示窗口的右边界。
3. 初始化变量 `ans` 为 0，用于记录最长不重复子串的长度。
4. 进入一个循环，循环变量 `i` 表示窗口的左边界，从 0 开始逐步向右移动。
5. 在每次循环开始时，将窗口中最左边的字符从 `checked` 集合中移除，表示将左边界向右移动一位。
6. 在循环内部，使用一个 `while` 循环，不断将窗口的右边界向右移动，直到窗口中出现了重复的字符或者到达字符串末尾。
7. 在 `while` 循环中，首先判断右边界的下一个字符是否在 `checked` 集合中，如果不在，则将其加入到 `checked` 集合中，并将右边界向右移动一位。
8. 更新 `ans` 的值，使用 `Math.max` 函数比较当前的最长子串长度和之前的最长子串长度，取较大值。
9. 循环结束后，返回 `ans`，即最长不重复子串的长度。

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Set<Character> checked = new HashSet<>();
        int len = s.length();
        int right = -1;
        int ans = 0;
        for (int i = 0; i < len; i++) { //i is the left pointer
            if (i != 0) {
                checked.remove(s.charAt(i - 1));
            }
            while (right + 1 < len && !checked.contains(s.charAt(right + 1))) {
                checked.add(s.charAt(right + 1));
                right += 1; 
            }
            ans = Math.max(ans, right - i + 1);
        }
        return ans;
    }
}
```



#### 反转链表

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        /**recursion */
        if (head == null || head.next == null) {
            return head;
        }
        ListNode ans = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return ans;

        /**iteration */
        // ListNode prev = null;
        // ListNode curr = head;
        // while (curr != null) {
        //     ListNode temp = curr.next;
        //     curr.next = prev;
        //     prev = curr;
        //     curr = temp;
        // }
        // return prev;
    }
}
```



## Network & Web

### 1. 友好的引入：HTTP & HTTPS简介

什么是**web**：the web is not the internet. wet is a collection of data and services! 而data on a webpage can contain: HTML, CSS, JavaScript.

**URLs**: how do we uniquely identify a piece of data on the web?

**HTTP** (Hypertext Transfer Protocol): How do web browsers communicate with web servers? HTTP is a protocol used to request and retrieve data from a web server.

**HTTPS**: a secure version of HTTP, it uses cryptography to secure data. / the HTTP protocol run over TLS. In contrast, HTTP runs over plain TCP, with no TLS added.

<font color = orange>说到了这里，你会觉得，要了解HTTP协议，就要先复习一下TCP/IP协议。</font>

### 2. TCP , UDP

为什么需要TCP：TCP是为了解决IP协议 unreliable的问题。IP is ==unreliable== and ==only provides a best effort== delivery service, which means: Packets may be lost (dropped), corrupted, or deliverd out of order.

**TCP** （Transmission Control Protocal）： TCP协议是一种面向字节流的协议，它将应用层传递的数据划分为适当大小的数据块，并封装成TCP报文段进行传输。TCP还提供了可靠的错误检测和流量控制等机制，以应对不同网络环境下的各种问题，并确保数据的可靠交付。TCP provides a byte stream abstraction, ordering, reliability, and ports:

- TCP auomatically breaks streams into segments.
- Segments contain sequence numbers, so the destination can reassemble the stream in order.
- The destination sends acknowledgements (ACKs) for each sequence number received. If the source doesn't receive the ACK, the source sends the packet again.
- Multiple services can share the same IP addreess by using different ports. (我们的电脑可以同时开很多页面)

TCP的**三次握手**（3-way handshake）: 是指建立一个TCP连接时，客户端和服务器它们之前会发送3个包。

TCP的三次握手是建立TCP连接的过程，确保发送方和接收方之间的通信能够可靠地进行。以下是TCP三次握手的步骤：

1. 第一次握手（SYN）：

   - 客户端（发送方）向服务器（接收方）发送一个带有SYN（同步）标志的TCP报文段。
   - 客户端==选择一个随机的初始序列号（ISN）并将其放入报文段的序列号字段==。
   - 客户端进入SYN_SENT（同步已发送）状态，等待服务器的响应。

2. 第二次握手（SYN + ACK）：

   - 服务器收到客户端的SYN报文段后，确认客户端的请求。
   - 服务器向客户端发送一个带有SYN和ACK（确认）标志的TCP报文段。
   - 服务器选择一个随机的初始序列号并将其放入报文段的序列号字段，同时==将客户端的序列号加1==作为确认号放入报文段的确认号字段。
   - 服务器进入SYN_RECEIVED（同步已接收）状态。

3. 第三次握手（ACK）：

   - 客户端收到服务器的SYN + ACK报文段后，确认服务器的响应。
   - 客户端向服务器发送一个带有ACK标志的TCP报文段。
   - 报文段的序列号字段设置为收到的确认号，确认号字段设置为收到的序列号加1。
   - 客户端进入ESTABLISHED（已建立）状态，服务器接收到这个ACK后也进入ESTABLISHED状态。
   - 此时，TCP连接已经建立，双方可以开始进行数据传输。

   可能的追问：如果**第三次ack时丢失**怎么办？——**TCP的重传**机制（Retransmission）<font color = orange>见161 lecture 18 5/8 这里先不写了</font>

3-way handshake is a process that ==establishes a reliable connection between two devices==, typically a client and a server, before they can exchange data. It is a three-step process that requires both the client and server to exchange synchronization and acknowledgment packets before the real data communication process starts.

Here's a step-by-step explanation of the TCP 3-way handshake process:

1. **Client Sends a SYN (Synchronize) Packet, Seq = x**: When the client wants to initiate a connection with the server it sends a TCP packet with the `SYN` flag set to the server indicating the client's intent to establish a connection.
2. **Server Responds with SYN-ACK Packet, Seq = y, Ack = x + 1**: Upon receiving the `SYN` packet, the server acknowledges the client's request by sending a TCP packet back. This packet has the `SYN` and `ACK` (Acknowledge) flags set. The `ACK` flag indicates the server's acknowledgment of the client's request, and the `SYN` flag indicates its intent to establish a connection.
3. **Client Acknowledges with an ACK Packet, Seq = x + 1, Ack = y + 1**: Once the client receives the `SYN-ACK` packet from the server, it sends an acknowledgment (`ACK`) packet back to the server. This packet has the `ACK` flag set and acknowledges the receipt of the server's response.

> **SYN (Synchronize)**: Synchronize Sequence Number. Indicates the start of a connection request.

> **ACK (Acknowledge)**: Acknowledges the receipt of a packet or confirms a connection establishment.

After the 3-way handshake is complete, both the client and server can start exchanging data in a reliable and orderly manner. If any of the packets in the handshake process are lost, the sender will retransmit them until a successful handshake is established.

TCP的**四次挥手**：

**UDP** (User Datagram Protocol):  no reliability. 比TCP快，因为无需三次握手；easy to spoof, 因为no Seq number. Usually used by low-latency, high-speed applications where errors are okay (e.g. video streaming, games)

**TCP和UDP**的区别：

1. 连接方式：TCP是面向连接的协议，而UDP是无连接的协议。TCP在通信之前需要建立连接，而UDP直接将数据报文发送给接收方，无需建立连接。
2. 可靠性：TCP提供可靠的数据传输，通过序列号、确认应答和重传等机制确保数据的完整性和正确性。UDP不提供这些机制，发送的数据报文可能丢失、重复、乱序或损坏，接收方无法检测到这些问题。
3. 流量控制和拥塞控制：TCP通过滑动窗口和拥塞控制算法来进行流量控制和拥塞控制，避免数据过载引起的性能问题。UDP没有这些机制，发送方可以以任意速率发送数据，可能导致网络拥塞和丢包。
4. 头部开销：TCP的头部较为复杂，包含序列号、确认号、窗口大小等信息，导致较大的头部开销。UDP的头部相对简单，只包含源端口号和目标端口号，开销较小。
5. 应用场景：由于TCP提供可靠性和数据顺序保证的特性，适用于需要可靠数据传输的应用，如文件传输、邮件传输、网页浏览等。UDP适用于对实时性要求较高、数据丢失可以容忍的应用，如音频、视频流传输、实时游戏等。

总结起来，TCP是一种面向连接、可靠的传输协议，提供可靠性、流量控制和拥塞控制等机制。UDP是一种无连接的传输协议，不提供可靠性和流控制，但具有低开销和快速传输的特点。选择使用TCP还是UDP取决于应用的需求，需要权衡可靠性、延迟和开销等因素。

<font color = orange>Now let's back to HTTP.</font>

### 3. HTTP请求头中的**Connection: keep-alive**的作用：

"Keep-Alive"是HTTP协议中的一个机制，用于在单个TCP连接上进行多个HTTP请求和响应，而不必每次都建立和关闭连接。它的作用是减少连接建立和关闭的开销，提高网络性能和效率。

当客户端发送一个带有"Keep-Alive"头字段的HTTP请求时，它告知服务器希望保持与服务器的连接长时间打开。服务器可以选择接受或拒绝这个请求。

如果服务器接受了"Keep-Alive"请求，那么在响应中将包含一个"Connection"头字段，其值为"keep-alive"，用于告知客户端继续使用同一TCP连接进行后续的请求和响应。

通过使用"Keep-Alive"，可以避免为每个请求都建立新的TCP连接，从而减少了连接建立和关闭的开销。这对于减少网络延迟和提高性能非常有益，尤其在多个请求需要连续发送的情况下，如网页中加载多个资源（图片、CSS、JavaScript等）。

需要注意的是，"Keep-Alive"并不是永久保持连接的机制。它仅表示客户端希望保持连接一段时间，而服务器可以根据自身配置或其他因素来决定关闭连接的时间。此外，HTTP/1.1默认启用了"Keep-Alive"机制，而HTTP/1.0则需要明确指定"Connection: keep-alive"头字段来启用。

可以拓展一下：How **HTTP/2** made keep-alive unnecessary ?

**Multiplexing:** Multiple requests and responses can be multiplexed over a single TCP connection. This means that instead of sending requests sequentially, multiple requests can be sent concurrently, and their corresponding responses can be received in any order.

**Header Compression:** Header compression techniques significantly reduce the size of headers sent with each request and response.

**Prioritization:** Clients can specify the priority of requests, indicating which resources are more important. Servers can use this information to prioritize the delivery of critical assets

**Server Push:** This allows the server to proactively send resources to the client before the client requests them.

### 4. Get 和 Post的区别



### 5. http2.0与http1.0的差别在哪里 

### 6. HTTP/3   

### 7. HTTPS 和HTTP的区别， 对称加密&非对称加密 

**对称加密**：通信双方用同样的key来进行加密和解密。特点：简单、性能好，但是存在密钥配送的问题：首次把密钥发给对方时，很容易被攻击者拦截。

**非对称加密**：通过公钥加密、私钥解密的方式，避免了密钥再配送过程中被盗取的问题。但是这一过程也存在隐患（==中间人攻击==）：因为非对称加密中，公钥是公开的，攻击者完全可以伪装成通信的一方把自己的公钥散播出去。这一问题的本质就是，A和B通信，A要如何验证自己拿到的B的公钥真的是B的公钥，而不是某个邪恶的人冒充的公钥。——解决方式是CA证书，它是用来证明公钥身份的合法性的。

而证书中除了有B的公钥信息，还有认证机构对于B的公钥信息生成的数字签名（CA对证书的摘要进行Hash后用CA的私钥加密得到的数字签名）。A收到B的证书以后，用同样的Hash算法生成证书的摘要，再用CA的公钥对数字签名进行解密，通过对比两份信息摘要就可以知道，这个证书到底有没有被中间人篡改过。

非对称加密虽然安全性更高，但是速度慢，影响性能。可以结合两种加密方式：把对称加密的key用非对称加密的公钥进行加密，然后发送出去，接收方用私钥进行解密从而得到对称加密的key，然后双方可以对称加密来进行沟通。

### 8. TLS 

TLS（Transport Layer Security）是一种加密协议，用于在计算机网络上提供安全的通信。建立在TCP的基础上，提供confidentiality + integrity。



### 9. OSI五层模型， 每一层 的作用

应用层：提供了网络服务和应用程序之间的接口。包括各种应用层协议，如 HTTP、FTP、DNS 等，用于实现特定的网络应用和服务。处理用户数据和用户与网络的交互，提供了高层抽象和用户接口。

传输层：提供了端到端的可靠数据传输服务。通过端口号标识应用程序，进行数据分段（Segmentation）和重组。提供了错误检测和纠正、流量控制、拥塞控制等功能。

网络层：负责在不同网络之间进行数据包（Packet）的路由和转发。使用路由器进行数据包的传输和路径选择，提供了寻址和定位服务，通过 IP 地址标识网络上的主机和网络。

数据链路层 （ARP, NAT, DNS, 以太网）：处理相邻节点之间的通信，通过物理地址（MAC 地址）标识网络上的设备 + 提供了可靠的点对点数据传输，将物理层提供的比特流划分为数据帧（Frames）。进行帧的同步、流量控制、差错检测和纠正等操作。

物理层：通过物理媒介传输比特流（Bits）的原始数据



### 10. DNS

DNS（Domain Name System）是互联网上用于将域名（如example.com）转换为对应 IP 地址的分布式命名系统。它充当了互联网中的“电话簿”，帮助用户通过易于记忆的域名访问网站，而无需记住复杂的数字 IP 地址。

DNS 的主要功能包括：

1. 域名解析：DNS 将用户输入的域名转换为对应的 IP 地址。当用户在浏览器中输入一个域名时，浏览器会向本地 DNS 解析器发送解析请求，解析器会查询 DNS 服务器以获取该域名对应的 IP 地址，并返回给浏览器，使其可以建立连接。
2. 分布式数据库：DNS 采用分布式数据库的方式存储域名和 IP 地址的映射关系。全球范围内存在多个 DNS 服务器，在层次化的结构中，顶层 DNS 服务器存储着顶级域名（如.com、.org）的信息，而下层的 DNS 服务器存储着更具体的域名信息。
3. 缓存机制：DNS 解析器通常会缓存解析结果，以减少对 DNS 服务器的查询次数。当用户再次访问相同的域名时，解析器可以直接从缓存中获取解析结果，提高解析速度。
4. 递归查询：当本地 DNS 解析器无法直接获取域名的解析结果时，它会向上层 DNS 服务器发起递归查询。递归查询是指解析器会一层层地向上查询，直到找到负责该域名的 DNS 服务器，并获取解析结果。
5. 反向解析：除了将域名解析为 IP 地址外，DNS 还支持反向解析，即通过已知的 IP 地址查找对应的域名。这在一些安全审计和网络故障排查中很有用。

DNS 在互联网通信中起着至关重要的作用，它使得用户能够使用便于记忆的域名来访问网站，同时也为网络服务提供商、网站管理员和网络工程师提供了管理和配置域名的机制。

### 11. XSS 

XSS（Cross-Site Scripting）是一种常见的网络安全漏洞，它允许攻击者将恶意脚本注入到受信任网站的页面中，并在用户的浏览器上执行这些脚本。这种攻击利用了网站对用户输入的信任，从而导致恶意脚本在用户浏览器中执行，可能导致信息泄露、会话劫持、恶意操作和其他安全问题。

XSS 攻击的基本过程如下：

1. 攻击者找到一个存在 XSS 漏洞的受信任网站，通常是在用户输入的地方未进行适当的验证和过滤。
2. 攻击者在受信任网站的输入字段或参数中注入恶意脚本，例如 JavaScript 代码。
3. 用户访问受攻击的网页时，网站将恶意脚本返回给用户的浏览器，浏览器会执行该脚本。
4. 恶意脚本可以访问用户的敏感信息、修改页面内容、劫持用户会话，或者执行其他恶意操作。

XSS 攻击可以分为以下几种类型：

1. 存储型 XSS：恶意脚本被存储在目标网站的服务器上，当其他用户访问包含恶意脚本的页面时，脚本会被返回并在其浏览器中执行。
2. 反射型 XSS：恶意脚本作为参数包含在 URL 中，当用户点击包含恶意脚本的恶意链接时，脚本会被返回并在其浏览器中执行。
3. DOM 型 XSS：恶意脚本通过修改页面的 DOM 结构来执行攻击，而不是通过服务器返回的内容。这种漏洞常见于使用 JavaScript 动态修改页面内容的应用程序。

为了防止 XSS 攻击，开发人员可以采取以下措施：

- 输入验证和过滤：对用户输入的数据进行验证和过滤，确保其符合预期的格式和内容，并移除或转义潜在的恶意代码。
- 输出转义：在将用户输入的数据插入到网页中时，对特殊字符进行转义，使其成为无害的文本，而不是可执行的代码。
- 使用安全的开发框架和库：使用经过安全审计和测试的开发框架和库，它们通常提供了内置的 XSS 防护机制。
- 设置合适的 HTTP 头：通过设置合适的 Content-Security-Policy（CSP）和 X-XSS-Protection 等 HTTP 头，可以增强浏览器的安全性，减少 XSS 攻击的风险。

总之，XSS 是一种利用受信任网站对用户输入的信任进行攻击的安全漏洞，开发人员应采取适当的防护措施来过滤和转义用户输入，并确保网站的安全性。用户也应保持浏览器和插件的更新，以减少受到 XSS 攻击的风险。

### 12.CSRF 

CSRF（Cross-Site Request Forgery），中文称为跨站请求伪造，是一种常见的网络安全攻击方式。它利用了网站对用户请求的信任，通过诱使用户在受信任网站上执行恶意操作，从而在用户不知情的情况下发送伪造的请求。

CSRF 攻击的基本过程如下：

1. 攻击者创建一个恶意网站或在合法网站上注入恶意代码。
2. 用户访问受攻击网站，并在同一浏览器中保持登录状态。
3. 在用户不知情的情况下，恶意代码发送伪造的请求，向目标网站发送恶意操作。这些请求通常包含用户的身份认证信息（如 Cookie）。
4. 目标网站认为这些请求是合法的，由于用户已经在该网站上登录，所以会执行相应的操作。
5. 攻击者成功地利用了用户在目标网站上的身份，执行了未经授权的操作。

CSRF 攻击可以导致一系列的问题，包括但不限于：

- 盗取用户身份，执行未授权的操作。
- 修改用户的个人信息或账户设置。
- 在用户不知情的情况下进行资金转账或购买。
- 利用用户权限在目标网站上进行恶意操作。
- 窃取用户的敏感信息等。

为了防止 CSRF 攻击，开发人员可以采取以下措施：

- 验证请求来源：在处理用户请求时，验证请求的来源是否是合法的网站，可以使用 CSRF Token 或同源检查等机制。
- 使用随机化的 CSRF Token：为每个用户会话生成一个随机的 CSRF Token，并将其嵌入表单或请求中，确保每个请求都带有有效的 Token。
- 限制敏感操作：对于执行敏感操作（如修改密码、支付等），要求用户进行额外的身份验证，例如输入密码或使用双因素身份验证。

综上所述，CSRF 是一种利用网站对用户请求的信任进行攻击的安全漏洞，开发人员应采取相应的防护措施来保护网站和用户的安全。

### 13. 跨域



>
> 12.static关键字，作用。（用在静态代码块，没答太好）

> 1.最近面试多吗，面试情况怎么样
>
> 大前天开始投简历，今天是我这个秋天的第一个面试
>
> 2.自我介绍
>
> 3.为什么来前端
>
> 最开始我想做一个自己的blog，所以开始接触一些前端很基本的知识，再了解发现前端涉及到的内容非常广，也很有趣
>
> 4.怎么自学的
>
> 我喜欢好几个途径交叉（比如好的教材、评价好的视频教程、写得比较清楚的官方文档、好的前辈的博客）对比着学，这样比较容易查漏补缺，然后很重要的内容也会在这个过程中被重复然后加深印象
>
> 5.你觉得自己对前端的掌握在什么等级
>
> 初级，很多知识因为没有实践的场景，很难说我理解地有多深刻；然后不去实践，很多细节我也根本不会注意到。但是我觉得我有很聪明的脑子，也很勤奋，只要给我一个专心钻研的机会，我会进步地很快的。
>
> 6.你觉得你掌握的最好的技术栈 
>
> 现在可能谈不上掌握得最好的，前端相关的react是我最近开始学习的，然后平时我用Java比较多，我特别喜欢我用java写的一个项目，就是gitlet，如果您有兴趣我特别想给您介绍一下。
>
> 7.简单介绍一下vue3这个框架
>
> 8.vue对于在双向绑定时怎么处理数组和对象
>
> 9.vue3是怎么实现双向绑定的
>
> 10.vue2和vue3的不同点
>
> 11.vue3怎么实现按需引入，怎么来按需引入的？
>
> 12.在前端工程领域中怎么做到依赖包的按需引入
>
> 答的webpack
>
> 13.webpack整个的构建流程是怎么样的
>
> 14.vue3中的proxy中的reflet
>
> 15.计算属性computed和watch有什么区别
>
> 16.vue的生命周期
>
> 17.组件在封装时需要遵循什么原则
>
> 18.什么样的组件算得上好用
>
> 19.pc端和移动端怎么去适配
>
> 20.弹性布局了解吗
>
> 21.简单介绍一下弹性布局
>
> 22.简单介绍一下盒模型
>
> 

> 1.vue2/3的区别
> 2.数据响应原理
>
> 3.flex布局
>
> 5.阻止冒泡事件
> 6.vue router生命周期
> 7.轮询
>

> 自我介绍
> 1.登陆的token是怎么配置的，专门配置的，还是放在哪里的
> 2.v-if和v-show的区别？就是那个display那一问题
>
> 5.跨域是什么？怎么解决？
> 6.cros是什么，具体是什么实现的
>
> 8.axios
> 9.token是怎么来的 添加在head头中？
> 10.token作为参数带过去的还是专门配置的
> 11.每次登陆都要发送请求token嘛
> 12.axios请求拦截与token的关系
> 13.http1.1、http2.0是长连接嘛？怎么实现的？
> 14.304的状态码是什么意思？
> 15.缓存有什么？
> 16.sessionStorage与loacalstorage的区别？
> 17.我关闭了浏览器的页面，sessionstorage的数据发生什么变化？localstorage的数据又有什么变化
> 18.vue3有了解嘛？
> 19.数据监听？有什么方法？
> 20.数据监听具体是怎么实现的？变化？
> 21.通过索引去会改变那个值？
> 22.重新添加的属性，会被监听到嘛？(面试官说的是不会）

> 1、介绍项目，其中有哪些困难点，怎么解决的 
>
> 2、position各个属性
>
> 3、说一说闭包，闭包的应用 
>
> 4、作用域 
>
> 7、用原型实现构造函数 



#### git指令有哪些



