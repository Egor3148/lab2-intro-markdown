# AEZAKMI
![Image of Sentrytocat](https://octodex.github.com/images/Sentrytocat_octodex.jpg)
```asm
.model small

.stack 100h

.data
    freq dw 4560, 3834, 3416, 3224, 3416, 3834, 4560, 5119, 4063, 4560
    dur dw 10, 10, 10, 10, 10, 10, 25, 5, 5, 20
    i db 0
    string db "          @@@@@       ",0Dh,0Ah,"         @@    @@     ",0Dh,0Ah,"       @@@      @@    ",0Dh,0Ah,"      @@  @@@@@  @@   ",0Dh,0Ah,"      @ @@.... @  @   ",0Dh,0Ah,"      @ @*.**.. @ @@@ ",0Dh,0Ah,"     @@  @*****@  @  @",0Dh,0Ah,"     @    @@@@@   @  @",0Dh,0Ah,"     @            @  @",0Dh,0Ah,"     @     @@@    @  @",0Dh,0Ah,"     @    @@ @    @@@ ",0Dh,0Ah,"    @@   @@  @    @   ",0Dh,0Ah,"    @    @   @    @   ",0Dh,0Ah,"    @    @  @@    @   ",0Dh,0Ah,"   @    @   @     @   ",0Dh,0Ah,"  @@@@@@@  @@@@@@@@   $",
    
.code

beep proc
        mov     al, 182         
        out     43h, al        
        push    bx
        mov     bx, dx
        mov     ax, [freq+bx]        
        pop     bx                        
        
        out     42h, al         
        mov     al, ah         
        out     42h, al 
        in      al, 61h         
                                
        or      al, 00000011b  
        out     61h, al     
        push    ax
        mov     bx, dx
        mov     ax, [dur+bx]      
        mov     bx, ax
        pop     ax
.pause1:
        mov     cx, 65535
.pause2:
        dec     cx
        jne     .pause2
        dec     bx
        jne     .pause1
        in      al, 61h         
                              
        and     al, 11111100b   
        out     61h, al         
    ret
beep endp

main:
        mov ax, @data
        mov ds, ax
        
        lea dx, string
        mov ah, 9
        int 21h
        
        mov cx, 10
        mov dx, 0
    cycle:
        push cx
        call beep
        inc dx
        inc dx
        pop cx
        loop cycle
        
        mov ax,4c00h
        int 21h
end main
```
- [ ] Complete this course
- [ ] Complete lab2
- [ ] Analyze the piece of code above
- [ ] Survive
