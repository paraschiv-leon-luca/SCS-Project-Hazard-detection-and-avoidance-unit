<h1>SCS Project - Hazard Detection and Avoidance Unit for Pipeline Architectures</h1>

<h2>1. Introduction</h2>

<h3>a. The Problem</h3>
<p>Instruction pipelining significantly increases processor throughput by concurently executing multiple instructions across distinct stages: Instruction Fetch (IF), Instruction Decode (ID), Execution (EX), Memory Access (MEM), and Writeback (WB). However, this concurrency introduces data hazards, specifically Read-After-Write (RAW) hazards, where an instruction attempts to read a register before a preceding instruction has written its updated result back. For example, if <code>ADD R1, R2, R3</code> is immediately followed by <code>SUB R4, R2, R1</code>, the subtraction instruction fetches an outdated value from <code>R1</code> during its decode stage because the addition has not yet reached the writeback stage. [1, page 298]</p>

<h3>b. Motivation</h3>
<p>Unresolved pipeline hazards lead directly to silent data corruption, invalid execution states, and unpredictable program behavior. Solving this problem at the hardware level is essential to guarantee instruction-level correctness while preserving the high clock speeds and throughput advantages of pipelined processor architectures.</p>

<h3>c. Objectives</h3>
<p><strong>Main Objective:</strong> Design, build, and test a hardware Hazard Detection and Avoidance Unit for a 5-stage pipelined processor.</p>
<p><strong>Secondary Objectives:</strong></p>
<ul>
  <li>Analyze data and control dependencies across the 5-stage pipeline to identify all hazard conditions.</li>
  <li>Design a Data Forwarding (Bypassing) Unit to route ALU results directly from the EX/MEM and MEM/WB pipeline registers back to the ALU inputs.</li>
  <li>Design a Hazard Detection Unit to stall the pipeline and insert hardware bubbles (NOPs) when encountering load-use hazards.</li>
  <li>Integrate both modules into the processor datapath and test functionality.</li>
</ul>

<h2>2. Bibliographic Study</h2>

<h3>a. Theoretical Concepts</h3>
<p>Pipelining divides instruction execution into sequential stages separated by pipeline registers [1, page 298]. Ideally, a pipeline completes one instruction per clock cycle (CPI = 1). This ideal flow is disrupted by 3 categories of hazards [1, page 290]:</p>
<ul>
  <li><strong>Structural Hazards:</strong> Hardware resource conflicts when two instructions require the same component simultaneously [1, page 290].</li>
  <li><strong>Data Hazards:</strong> Data dependencies between instructions, categorized as Read-After-Write (RAW, true dependency), Write-After-Read (WAR, anti-dependency), and Write-After-Write (WAW, output dependency). [1, page 290]</li>
  <li><strong>Control Hazards </strong>: Latencies introduced by branch and jump instructions when the instruction fetch address cannot be determined in time.</li>
</ul>

<h3>b. Existing Approaches and Critical Comparison</h3>
<ul>
  <li><strong>Hardware Pipeline Interlocks (Stalling) [1, page 315]:</strong> Hardware detects dependencies and freezes earlier pipeline stages until the required register writeback completes.
    <br>Advantages: Ensures software transparency and execution correctness without compiler intervention.
    <br>Disadvantages: Degrades performance by introducing delays for every data dependency.</li>
  <li><strong>Data Forwarding (Bypassing) [1, page 315]:</strong> Hardware routes intermediate results from later pipeline buffers directly to earlier execution stages before formal register file writeback.
    <br>Advantages: Eliminates stalls for standard ALU-to-ALU dependencies, maintaining high throughput.
    <br>Disadvantages: Increases hardware complexity.</li>
</ul>

<h2>3. Work Plan</h2>
<ul>
  <li><strong>Meeting 1:</strong> Pick project.</li>
  <li><strong>Meeting 2:</strong> Study the main contents of the project.</li>
  <li><strong>Meeting 3:</strong>  Sketch out the forwarding unit and draft its truth tables.</li>
  <li><strong>Meeting 4:</strong> Build the stall logic for load-use hazards and handle pipeline flushes.</li>
  <li><strong>Meeting 5:</strong> Integrate both units to the CPU and test if everything works together.</li>
  <li><strong>Meeting 6: </strong>
  Check timing, run performance tests, and finish the documentation. </li>
  <li><strong>Meeting 7: </strong>
  Main presentation, testing and evaluation.
</ul>

<h2>4. Bibliography</h2>
<ol>
  <li>D. A. Patterson and J. L. Hennessy, Computer Organization and Design: The Hardware/Software Interface, 6th ed. San Francisco, CA: Morgan Kaufmann, 2020.</li>
</ol>
