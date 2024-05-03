.data
mensagem: .asciiz "\nSelecione opcao[1 para soma, 2 para subtacao, 3 para multiplicacao e 4 para divisao]\n\0"
mensagemf: .asciiz "\nMais uma operacao? 1 para sim e 0 para nao\n"
.text
.globl main
wrap:

main:  
	la $a0, mensagem
	li $v0, 4
	syscall
    li $v0, 5
    li $t1, 0
    syscall #syscall
    
loop:
    addi $t1, $t1, 1
    beq $t1, $v0, sum
    addi $t1, $t1, 1
    beq $t1, $v0, subt
    addi $t1, $t1, 1
    beq $t1, $v0, multp
    addi $t1, $t1, 1
    beq $t1, $v0, divd
    j main
    
sum:
	li $v0, 5
	syscall
	move $t1, $v0
	li $v0, 5
	syscall
	move $t2, $v0
	add $a0, $t1, $t2
	li $v0, 1
	syscall
	j fim
	
subt:
	li $v0, 5
	syscall
	move $t1, $v0
	li $v0, 5
	syscall
	move $t2, $v0
	sub $a0, $t1, $t2
	li $v0, 1
	syscall
	j fim

multp:
	li $v0, 5
	syscall
	move $t1, $v0
	li $v0, 5
	syscall
	move $t2, $v0
	mult  $t1, $t2
	mflo $a0
	li $v0, 1
	syscall
	j fim
	
divd:
	li $v0, 5
	syscall
	move $t1, $v0
	li $v0, 5
	syscall
	move $t2, $v0
	div $a0, $t1, $t2
	li $v0, 1
	syscall
    j fim 
             
fim:  
	la $a0, mensagemf
	li $v0, 4
	syscall
	li $v0, 5
	syscall
	beq $v0, 1, wrap

    li $v0, 10             # Encerra o programa
    syscall
