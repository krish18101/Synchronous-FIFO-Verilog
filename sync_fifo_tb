`timescale 1ns / 1ps
//////////////////////////////////////////////////////////////////////////////////
// Company: 
// Engineer: 
// 
// Create Date: 02.01.2026 00:00:57
// Design Name: 
// Module Name: sync_fifo_tb
// Project Name: 
// Target Devices: 
// Tool Versions: 
// Description: 
// 
// Dependencies: 
// 
// Revision:
// Revision 0.01 - File Created
// Additional Comments:
// 
//////////////////////////////////////////////////////////////////////////////////


module sync_fifo_tb();
parameter fifo_depth = 8;
parameter data_width = 32;
reg clk = 0;
reg rst , cs , wr_en , rd_en ;
reg [data_width-1:0] data_in;
wire [data_width-1:0] data_out;
 wire empty , full;
 integer i  ;
 
 sync_fifo
 #(.fifo_depth(fifo_depth),
 .data_width(data_width))
 
 dut
 (.clk (clk),
 .rst(rst) ,
 .cs(cs) ,
 .wr_en( wr_en) ,
 .rd_en(rd_en),
 .data_in(data_in),
 .data_out(data_out),
 .empty(empty),
 .full(full));
 
 always
  begin 
 #5 clk = ~clk;
  end
  
  task write_data(input [data_width-1:0] d_in);
  begin 
  @(posedge clk);
  cs = 1;
  wr_en = 1;
  data_in = d_in;
  $display($time, "write_data = %0d" , data_in);
  @(posedge clk);
  cs = 1 ; wr_en = 0;
  end
  endtask
  
  task read_data();
  begin @(posedge clk);
  cs = 1; rd_en = 1;
  @(posedge clk);
  $display($time , "read_data = %0d" , data_out);
  cs = 1; rd_en = 0;
  end
  endtask
  
  initial 
  begin
  #1;
  rst = 0;
  rd_en = 0;
  wr_en = 0;
  
  @(posedge clk)
  rst = 1;
  $display($time , "\n sceanrio 1");
  write_data(1);
  write_data(10);
  write_data(100);
  
  read_data();
  read_data();
  read_data();
  
   $display($time , "\n sceanrio 2");
   for(i= 0; i< fifo_depth ; i = i+1)
   begin
   write_data(2**i);
   end
   for(i= 0; i< fifo_depth ; i = i+1)
   begin
   read_data();
   end
   $display($time , "\n sceanrio 3");
   for(i= 0; i< fifo_depth ; i = i+1)
   begin
   write_data(2**i);
   read_data();
   end
   
   #40;
   end

initial begin
$dumpfile("dump.vcd"); $dumpvars;

   end
    
endmodule
