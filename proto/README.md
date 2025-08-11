# Protocol Buffer Definitions

This directory contains the Protocol Buffer definitions for the BasicTracer implementation.

## File Structure

- `wire.proto`: The protobuf definition file that defines the TracerState message used for trace propagation across process boundaries.

## Generating Python Code

To regenerate the `wire_pb2.py` file from the `wire.proto` definition, follow these steps:

### Prerequisites

- Create a virtual environment to isolate the protobuf version:
  ```
  python -m venv proto_venv
  source proto_venv/bin/activate
  ```
- Install the required packages:
  ```
  pip install 'protobuf==5.29.5' 'grpcio-tools<1.65.0'
  ```

### Generation Command

Run the following command from the root directory of the project (while in the virtual environment):

```bash
python -c "from grpc_tools import protoc; protoc.main(['', '-I=proto/', '--python_out=basictracer/', 'proto/wire.proto'])"
```

### Verification

After generating the file, verify that:

1. The file is created at `basictracer/wire_pb2.py`
2. The generated file includes a comment indicating the protobuf Python version (5.x)
3. The file correctly defines the `TracerState` message with its fields:
   - `trace_id`
   - `span_id`
   - `sampled`
   - `baggage_items` (map)

## Important Notes

- Do not manually edit the generated `wire_pb2.py` file as it will be overwritten when regenerated.
- If you modify `wire.proto`, you must regenerate the Python code.
- The generated code should be compatible with protobuf 5.29.5 as specified in the project's `setup.py` file.