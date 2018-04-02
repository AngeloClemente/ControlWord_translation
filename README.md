# ControlWord_translation

/* List that translates instruction's opcode to a ControlWord */
		// ControlWord: (28 bits) SA, SB, DA, RegWrite, MemWrite, FS, C0,EN_Mem, EN_ALU, Asel, Bsel, PS, EN_PC
		
	// Instruction // Opcode             // FORMAT // 32 bit instruction       
	

	      /*   ADD -- 10001011000(11bits) --   R    -- (op)10001011000 (Rm/SB)ddddd (shamt)xxxxxx (Rn/SA)ddddd (Rd/DA)ddddd 
			     (CONTROLWORD): SA= instr[9:5],
				                 SB= instr[20:16]
									  DA= instr[4:0]
									  RegWrite= 1
									  Memwrite= 0
				                 FS= 01000
									  C0= 0
									  EN_Mem= 0
									  EN_ALU = 1
									  Asel = 0
									  Bsel = 0
									  PS = 01
				  
				 
				  SUB -- 11001011000(11bits) --   R    -- (op)11001011000 (Rm/SB)ddddd (shamt)xxxxxx (Rn/SA)ddddd (Rd/DA)ddddd 
				  (CONTROLWORD): SA= instr[9:5]
				                 SB= instr[20:16]
									  DA= instr[4:0]
									  RegWrite= 1
									  Memwrite= 0
				                 FS= 01001
									  C0= 1
									  EN_Mem= 0
									  EN_ALU= 1
									  Asel = 0
									  Bsel= 0
									  PS = 01 
									  
			    ADDI -- 1001000100(10bits)  --   I    -- (op)1001000100 (I/const)12b'd (Rn)ddddd (Rd)ddddd
				 (CONTROLWORD):  SA= instr[9:5]
				                 SB= Don't care
									  DA= instr[4:0]
									  RegWrite= 1
									  Memwrite= 0
				                 FS= 01000
									  C0= 0
									  EN_Mem= 0
									  EN_ALU= 1
									  Asel = 0
									  Bsel= 1
									  PS = 01 
									  
	          SUBI -- 1101000100(10bits)  --   I    -- (op)1101000100 (I/const)12b'd (Rn)ddddd (Rd)ddddd
				 (CONTROLWORD):  SA= instr[9:5]
				                 SB= Don't care
									  DA= instr[4:0]
									  RegWrite= 1
									  Memwrite= 0
				                 FS= 01001
									  C0= 1
									  EN_Mem = 0
									  Asel = 0
									  EN_ALU= 1
									  Bsel= 1
									  PS = 01 
									  
             ADDS -- 10101011000(11bits) --   R   -- (op)10101011000 (Rm/SB)ddddd (shamt)xxxxxx (Rn/SA)ddddd (Rd/DA)ddddd 
				  
			    SUBS -- 11101011000(11bits) --   R   -- (op)11101011000 (Rm/SB)ddddd (shamt)xxxxxx (Rn/SA)ddddd (Rd/DA)ddddd 
				  
		   	 ADDIS -- 1001000100(10bits) --   I   -- (op)1001000100 (I/const)12b'd (Rn)ddddd (Rd)ddddd
				 
				 SUBIS -- 1111000100(10bits) --   I   -- (op)1111000100 (I/const)12b'd (Rn)ddddd (Rd)ddddd
				 
DATA TRANSFER /////////////////////////////////////////////////////////////////////////////////////////////////////////


				 STUR -- 11111000000(11bits) --   D   -- (op)11111000000 (MEM_address)9b'd (op2)00 (Rn)ddddd (Rt)ddddd
				 (CONTROLWORD):  SA= Instr[9:5]
				                 SB= Instr[4:0]
									  DA= Don't care (x)
									  RegWrite= 0
									  Memwrite= 1
				                 FS= 01000
									  C0= 0
									  EN_Mem= 0
									  EN_ALU= Don't care (x)
									  Asel = 0
									  Bsel= 1
									  PS = 01 
									  
				 LDUR -- 11111000010(11bits) --   D   -- (op)11111000010 (MEM_address)9b'd (op2)00 (Rn)ddddd (Rt)ddddd
				 (CONTROLWORD):  SA= Instr[4:0]
				                 SB= Don't care (x)
									  DA= Instr[9:5]
									  RegWrite= 1
									  Memwrite= 0
				                 FS= 01000
									  C0= 0
									  EN_Mem= 1
									  EN_ALU= 0
									  Asel = 0
									  Bsel = 1
									  PS = 01 
									 
				 STURB -- 00111000000(11bits) --   D   -- (op)00111000000 (MEM_address)9b'd (op2)00 (Rn)ddddd (Rt)ddddd
				 (CONTROLWORD):  SA= Instr[9:5]
				                 SB= Instr[4:0]
									  DA= Don't care (x)
									  RegWrite= 0
									  Memwrite= 1
				                 FS= 01000
									  C0= 0
									  EN_Mem= 0
									  EN_ALU= Don't care (x)
									  Asel = 0
									  Bsel= 1
									  PS = 01 
									  
				   LDURB -- 00111000010(11bits) --   D   -- (op)00111000010 (MEM_address)9b'd (op2)00 (Rn)ddddd (Rt)ddddd
					(CONTROLWORD):  SA= Instr[4:0]
				                 SB= Don't care (x)
									  DA= Instr[9:5]
									  RegWrite= 1
									  Memwrite= 0
				                 FS= 01000
									  C0= 0
									  EN_Mem= 1
									  EN_ALU= 0
									  Asel = 0
									  Bsel = 1
									  PS = 01 
									  
					MOVZ -- 110100101(9bits) --   IW   -- (op)110100101 (sh*16) 2b'dd (constant) 16'bd (Rd) 5'bd
					(CONTROLWORD):  SA= Zero Register (64)
				                 SB= Don't Care
									  DA= Instr[4:0]
									  RegWrite= 1
									  Memwrite= 0
				                 FS= 01000 (May have to shift)
									  C0 = 0
									  EN_Mem= 0
									  EN_ALU= 1
									  Asel = 0
									  Bsel = 1
									  PS = 01 
									  
					MOVK -- 111100101(9bits) --   IW   -- (op)111100101 (sh*16) 2b'dd (constant) 16'bd (Rd) 5'bd
					(CONTROLWORD):  SA= Zero Register (64)
				                 SB= Don't Care
									  DA= Instr[4:0]
									  RegWrite= 1
									  Memwrite= 0
				                 FS= 01000 (May have to shift)
									  C0 = 0
									  EN_Mem= 0
									  EN_ALU= 1
									  Asel = 0
									  Bsel = 1
									  PS = 01 
							
LOGIC  //////////////////////////////////////////////////////////////////////////////////////////////////////////////////


					AND -- 10001010000(11bits) --   R    -- (op)10001010000 (Rm/SB)ddddd (shamt)xxxxxx (Rn/SA)ddddd (Rd/DA)ddddd 
					(CONTROLWORD):  SA= Instr[9:5]
				                   SB= Instr[20:16]
									    DA= Instr[4:0]
									    RegWrite= 1
									    Memwrite= 0
				                   FS= 00000 
									    C0 = 0
									    EN_Mem= 0
									    EN_ALU= 1
									    Asel = 0
									    Bsel = 0
									    PS = 01 			
			
					ORR -- 10101010000(11bits) --   R    -- (op)10101010000 (Rm/SB)ddddd (shamt)xxxxxx (Rn/SA)ddddd (Rd/DA)ddddd 
					(CONTROLWORD):  SA= Instr[9:5]
				                   SB= Instr[20:16]
									    DA= Instr[4:0]
									    RegWrite= 1
									    Memwrite= 0
				                   FS= 00100 
									    C0 = 0
									    EN_Mem= 0
									    EN_ALU= 1
									    Asel = 0
									    Bsel = 0
									    PS = 01 	
										
					EOR -- 11001010000(11bits) --   R    -- (op)11001010000 (Rm/SB)ddddd (shamt)xxxxxx (Rn/SA)ddddd (Rd/DA)ddddd 
					(CONTROLWORD):  SA= Instr[9:5]
				                   SB= Instr[20:16]
									    DA= Instr[4:0]
									    RegWrite= 1
									    Memwrite= 0
				                   FS= 01100 
									    C0 = 0
									    EN_Mem= 0
									    EN_ALU= 1
									    Asel = 0
									    Bsel = 0
									    PS = 01 	 
										 
					ANDI -- 1001001000(10bits)  --   I    -- (op)1001001000 (I/const)12b'd (Rn)ddddd (Rd)ddddd
					(CONTROLWORD):  SA= Instr[9:5]
				                   SB= Don't care (x)
									    DA= Instr[4:0]
									    RegWrite= 1
									    Memwrite= 0
				                   FS= 00000 
									    C0 = 0
									    EN_Mem= 0
									    EN_ALU= 1
									    Asel = 0
									    Bsel = 1
									    PS = 01 	 
 
			     ORRI -- 1011001000(10bits)  --   I    -- (op)1011001000 (I/const)12b'd (Rn)ddddd (Rd)ddddd
				  (CONTROLWORD):   SA= Instr[9:5]
				                   SB= Don't care (x)
									    DA= Instr[4:0]
									    RegWrite= 1
									    Memwrite= 0
				                   FS= 00100 
									    C0 = 0
									    EN_Mem= 0
									    EN_ALU= 1
									    Asel = 0
									    Bsel = 1
									    PS = 01 	
										 
			     EORI -- 1101001000(10bits)  --   I    -- (op)1101001000 (I/const)12b'd (Rn)ddddd (Rd)ddddd
				  (CONTROLWORD):   SA= Instr[9:5]
				                   SB= Don't care (x)
									    DA= Instr[4:0]
									    RegWrite= 1
									    Memwrite= 0
				                   FS= 01100 
									    C0 = 0
									    EN_Mem= 0
									    EN_ALU= 1
									    Asel = 0
									    Bsel = 1
									    PS = 01 
										 
				  ANDS -- 11101010000(11bits) --   R    -- (op)11101010000 (Rm/SB)ddddd (shamt)xxxxxx (Rn/SA)ddddd (Rd/DA)ddddd 
					
			    ANDIS -- 1111001000(10bits)  --   I    -- (op)1111001000 (I/const)12b'd (Rn)ddddd (Rd)ddddd
				 
				  LSR -- 11010011010(11bits) --   R    -- (op)11010011010 (Rm/SB)ddddd (shamt)xxxxxx (Rn/SA)ddddd (Rd/DA)ddddd 
					(CONTROLWORD):  SA= Instr[9:5]
				                   SB= Don't care (x)
									    DA= Instr[4:0]
									    RegWrite= 1
									    Memwrite= 0
				                   FS= 10100 
									    C0 = 0
									    EN_Mem= 0
									    EN_ALU= 1
									    Asel = 0
									    Bsel = 1
									    PS = 01 	 
										 
				  LSL -- 11010011011(11bits) --   R    -- (op)11010011011 (Rm/SB)dd (shamt)dddddd (Rn/SA)ddddd (Rd/DA)ddddd 
					(CONTROLWORD):  SA= Instr[9:5]
				                   SB= Don't care (x)
									    DA= Instr[4:0] *Rd
									    RegWrite= 1
									    Memwrite= 0
				                   FS= 10000 
									    C0 = 0
									    EN_Mem= 0
									    EN_ALU= 1
									    Asel = 0
									    Bsel = 1
									    PS = 01 	 
										 
Conditional Branches ///////////////////////////////////////////////////////////////////////////////////////////////////////////

				  CBZ -- 10110100(8bits)    --   CB   -- (op)10110100 (Branch address/constant) 19'bd (Rt) 5'bddddd
					(CONTROLWORD):  SA= Don't Care
				                   SB= Instr[4:0] *Rt
									    DA= Don't care (x)
									    RegWrite= 0
									    Memwrite= 0
				                   FS= 00000 
									    C0 = 0
									    EN_Mem= 0
									    EN_ALU= 0
									    Asel = 1
									    Bsel = 0
									    PS = 11 	 
										 EN_PC = status (Z)
										 
				 CBNZ -- 10110101(8bits)    --   CB   -- (op)10110101 (Branch address/constant) 19'bd (Rt) 5'bddddd
					(CONTROLWORD):  SA= Don't Care
				                   SB= Instr[4:0] *Rt
									    DA= Don't care
									    RegWrite= 0
									    Memwrite= 0
				                   FS= 00000 
									    C0 = 0
									    EN_Mem= 0
									    EN_ALU= 0
									    Asel = 1
									    Bsel = 0
									    PS = 11 	 
										 EN_PC = status (~Z)
										 
				 Bcond. -- 10110100(8bits)    --   CB   -- (op)10110100 (Branch address) 19'bd (Rt) 5'bddddd									 
						

Unconditional Branches /////////////////////////////////////////////////////////////////////////////////////////////////////////
				 
				 
				 B -- 000101(6bits)      --   B    -- (op)000101 (Branch address/constant) 26'bd 
					(CONTROLWORD):  SA= Don't care (x)
				                   SB= Don't care (x)
									    DA= Don't care (x)
									    RegWrite= 0
									    Memwrite= 0
				                   FS= Don't care 
									    C0 = Don't care
									    EN_Mem= 0
									    EN_ALU= 0
									    Asel = 1
									    Bsel = Don't care (x)
									    PS = 10 	 
										 EN_PC = 1
										 
				 BL -- 100101(6bits)      --   B    -- (op)000101 (Branch address/constant) 26'bd 
					(CONTROLWORD):  SA= Don't care (x)
				                   SB= Don't care (x)
									    DA= Don't care (x)
									    RegWrite= 0
									    Memwrite= 0
				                   FS= Don't care 
									    C0 = Don't care
									    EN_Mem= 0
									    EN_ALU= 0
									    Asel = 1
									    Bsel = Don't care (x)
									    PS = 10 	 
										 EN_PC = 1
										 
										 
	
									  
							
									  
			*/
