## [[Robust IO Package]]
### $\text{rio\_readn}$
```c
#include <unistd.h>
#include <errno.h>

/*
 * rio_readn - Robustly read n bytes (unbuffered)
 */
ssize_t rio_readn(int fd, void *usrbuf, size_t n) {
    size_t nleft = n;           // 읽어야 할 남은 바이트 수
    ssize_t nread;              // 실제로 읽은 바이트 수
    char *bufp = usrbuf;        // 사용자 버퍼 포인터

    while (nleft > 0) {
        if ((nread = read(fd, bufp, nleft)) < 0) {
            if (errno == EINTR) // 신호 인터럽트로 인한 재시도
                nread = 0;
            else
                return -1;      // 읽기 오류 발생 시
        } else if (nread == 0)
            break;              // EOF 도달 시

        nleft -= nread;
        bufp += nread;
    }
    return (n - nleft);          // 실제로 읽은 바이트 수 반환, >= 0
}
```