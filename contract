pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract NFTContract is ERC721 {
    string public constant NFT_NAME = "NFT0";
    string public constant NFT_SYMBOL = "N0";

    uint256 private color = 0;

    constructor() ERC721(NFT_NAME, NFT_SYMBOL) {}

    function mint(address to) public {
        uint256 newTokenId = totalSupply();
        _mint(to, newTokenId);
    }

    function sendNFT(address to) public {
        uint256 tokenId = balanceOf(msg.sender) - 1;
        safeTransferFrom(msg.sender, to, tokenId);

        color++;

        uint256 totalSupply = totalSupply();
        for (uint256 i = 0; i < totalSupply; i++) {
            if (ownerOf(i) == msg.sender && i != tokenId) {
                // Modify the color of the existing NFTs owned by the sender
                _setTokenColor(i, color);
            }
        }

        // Mint a new NFT for the sender with the new color
        _mint(msg.sender, totalSupply());
        _setTokenColor(totalSupply(), color);
    }

    function _setTokenColor(uint256 tokenId, uint256 newColor) private {
        // Set the color of a token
        // Here, we just use the lowest 8 bits to store the color value
        _setTokenURI(tokenId, string(abi.encodePacked(_tokenURI(tokenId), "/", toString(newColor))));
    }

    function toString(uint256 value) private pure returns (string memory) {
        // Convert a uint256 value to a string
        if (value == 0) {
            return "0";
        }

        uint256 temp = value;
        uint256 digits;

        while (temp != 0) {
            digits++;
            temp /= 10;
        }

        bytes memory buffer = new bytes(digits);

        while (value != 0) {
            digits--;
            buffer[digits] = bytes1(uint8(48 + uint256(value % 10)));
            value /= 10;
        }

        return string(buffer);
    }
}
