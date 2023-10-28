# SO-Codes

Repository for codes used in Operational Systems including runtime capture, inter-process communication, threads, parallelism, and scheduling.
import sys

def extract_page_offset(virtual_address, page_size):
    page_number = virtual_address // page_size #divisao por interiro exemplo 5//2 = 2
    offset = virtual_address % page_size # pega o resto da divisao, exemplo 5%2 = 1
    return page_number, offset

def main(virtual_address, bits):
    if bits == 16:
        page_size = 256
    elif bits == 32:
        page_size = 4096
    else:
        raise ValueError("Diferente de 16 e 32 bits. Erro.")

    virtual_address = int(virtual_address)

    page_number, offset = extract_page_offset(virtual_address, page_size)
    data_memory_file = "data_memory.txt"  
    with open(data_memory_file, 'r') as file:
        lines = file.readlines()
        data_value = lines[page_number].strip()

    print(f"O endereco {virtual_address} contem:\n"
          f"numero da pagina = {page_number}\n"
          f"deslocamento = {offset}\n"
          f"Valor lido: {data_value}")

if __name__ == '__main__':
    if len(sys.argv) != 3:
        print("Erro")
        sys.exit(1)
    virtual_address = sys.argv[1]
    bits = int(sys.argv[2])
    main(virtual_address, bits)
